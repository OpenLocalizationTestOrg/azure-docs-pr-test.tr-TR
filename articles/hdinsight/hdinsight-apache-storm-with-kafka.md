---
title: "aaaUse hdınsight'ta - Azure Storm Apache Kafka | Microsoft Docs"
description: "Apache Kafka, Hdınsight üzerinde Apache Storm ile yüklenir. Storm ile sağlanan KafkaBolt ve KafkaSpout bileşenleri toowrite tooKafka ve kullanarak okuyun, gelen nasıl hello öğrenin. Ayrıca nasıl toouse Flux framework toodefine hello ve Storm topolojilerini gönderme öğrenin."
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
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="1c75f-105">Hdınsight üzerinde Storm ile Apache Kafka (Önizleme) kullanın</span><span class="sxs-lookup"><span data-stu-id="1c75f-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="1c75f-106">Bilgi nasıl toouse Apache Storm tooread gelen ve tooApache Kafka yazma.</span><span class="sxs-lookup"><span data-stu-id="1c75f-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="1c75f-107">Bu örnek ayrıca nasıl Storm topolojisini toohello HDFS uyumlu toosave verilerden dosya sistemi Hdınsight tarafından kullanılan gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="1c75f-108">Bu belgedeki Hello adımlar hem Hdınsight üzerinde Storm ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c75f-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="1c75f-109">Bu kümeleri, hem bir Azure sanal hello Storm kümesi toodirectly sağlayan ağ içinde bulunan Kafka küme hello ile iletişim ' dir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="1c75f-110">Bu belgedeki hello adımları tamamladığınızda, toodelete hello kümeleri tooavoid aşırı ücretleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1c75f-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="1c75f-111">Merhaba kod alın</span><span class="sxs-lookup"><span data-stu-id="1c75f-111">Get hello code</span></span>

<span data-ttu-id="1c75f-112">Bu belgede kullanılan hello örneğin Hello kod şu adreste [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="1c75f-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="1c75f-113">toocompile bu proje için geliştirme ortamınızı yapılandırma aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c75f-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="1c75f-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="1c75f-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="1c75f-115">Java 8 Hdınsight 3.5 veya daha yükseğini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="1c75f-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="1c75f-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="1c75f-117">Bir SSH istemcisi (Merhaba gereksinim `ssh` ve `scp` komutları) - bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1c75f-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="1c75f-118">Bir metin düzenleyicisi veya IDE.</span><span class="sxs-lookup"><span data-stu-id="1c75f-118">A text editor or IDE.</span></span>

<span data-ttu-id="1c75f-119">Geliştirme iş istasyonunuza Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="1c75f-120">Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="1c75f-121">`JAVA_HOME`-hello JDK yüklendiği toohello dizin işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="1c75f-122">`PATH`-yolları aşağıdaki hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="1c75f-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="1c75f-123">`JAVA_HOME`(veya eşdeğer yolu hello).</span><span class="sxs-lookup"><span data-stu-id="1c75f-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="1c75f-124">`JAVA_HOME\bin`(veya eşdeğer yolu hello).</span><span class="sxs-lookup"><span data-stu-id="1c75f-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="1c75f-125">Maven'ın yüklendiği başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="1c75f-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="1c75f-126">Merhaba kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c75f-126">Create hello clusters</span></span>

<span data-ttu-id="1c75f-127">Hdınsight üzerinde Apache Kafka sağlamaz erişim toohello Kafka aracıların üzerinden genel internet hello.</span><span class="sxs-lookup"><span data-stu-id="1c75f-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="1c75f-128">Merhaba düğümler aynı Azure sanal ağ konuşmaları tooKafka olmalıdır hello herhangi bir şey Kafka küme hello.</span><span class="sxs-lookup"><span data-stu-id="1c75f-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="1c75f-129">Bu örnekte, bir Azure sanal ağında hello Kafka ve Storm kümeleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="1c75f-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="1c75f-130">Merhaba Aşağıdaki diyagramda hello kümeleri arasında iletişimi nasıl akacağını gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1c75f-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Bir Azure sanal ağı Storm ve Kafka kümelerde diyagramı](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="1c75f-132">SSH ve Ambari üzerinden erişilebilen gibi diğer hizmetler hello kümede Internet hello.</span><span class="sxs-lookup"><span data-stu-id="1c75f-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="1c75f-133">Merhaba ortak bağlantı noktaları Hdınsight ile kullanılabilir hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="1c75f-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="1c75f-134">Azure sanal ağı, Kafka, oluşturabilir ve Storm el ile kümeleri olsa da, daha kolay toouse bir Azure Resource Manager şablonu durumdur.</span><span class="sxs-lookup"><span data-stu-id="1c75f-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="1c75f-135">Toodeploy Azure sanal ağı, Kafka, kullanım hello aşağıdaki adımları ve tooyour Azure aboneliği Storm kümeleri.</span><span class="sxs-lookup"><span data-stu-id="1c75f-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="1c75f-136">Düğme toosign tooAzure içinde ve açık hello şablonunda hello Azure portalı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c75f-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="1c75f-137">Hello Azure Resource Manager şablonu konumundadır **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="1c75f-138">Kaynakları aşağıdaki hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="1c75f-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="1c75f-139">Azure kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="1c75f-139">Azure resource group</span></span>
    * <span data-ttu-id="1c75f-140">Azure Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="1c75f-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="1c75f-141">Azure Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="1c75f-141">Azure Storage account</span></span>
    * <span data-ttu-id="1c75f-142">Hdınsight sürüm 3.6 (üç alt düğümleri) üzerindeki Kafka</span><span class="sxs-lookup"><span data-stu-id="1c75f-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="1c75f-143">Sürüm 3.6 (üç alt düğümler) hdınsight'ta Storm</span><span class="sxs-lookup"><span data-stu-id="1c75f-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="1c75f-144">Hdınsight üzerinde Kafka kullanılabilirliğini tooguarantee, kümenizi en az üç alt düğümleri içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="1c75f-145">Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1c75f-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="1c75f-146">Kılavuzu toopopulate hello girişleri hello üzerinde aşağıdaki kullanım hello **özel dağıtım** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="1c75f-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="1c75f-148">**Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="1c75f-149">Bu grup hello Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="1c75f-150">**Konum**: konum coğrafi olarak Kapat tooyou seçin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="1c75f-151">**Temel küme adı**: Bu değer hello Storm ve Kafka kümelerinin hello temel adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="1c75f-152">Örneğin, **hdı** adlı bir Storm kümesi oluşturur **storm hdı** ve adlı Kafka küme **kafka hdı**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="1c75f-153">**Oturum açma kullanıcı adı küme**: hello Storm ve Kafka kümelerinin hello Yöneticisi kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="1c75f-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="1c75f-154">**Oturum açma parolası küme**: hello Storm ve Kafka kümeleri için hello yönetici kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="1c75f-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="1c75f-155">**SSH kullanıcı adı**: hello Storm ve Kafka kümeleri için SSH kullanıcı toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="1c75f-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="1c75f-156">**SSH parolası**: hello SSH kullanıcı hello Storm ve Kafka kümelerinin hello parolası.</span><span class="sxs-lookup"><span data-stu-id="1c75f-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="1c75f-157">Okuma hello **hüküm ve koşullar**ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="1c75f-158">Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="1c75f-159">Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="1c75f-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="1c75f-160">Merhaba kaynakları oluşturduktan sonra hello dikey penceresinde hello kaynak grubu için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Kaynak grubu dikey hello vnet ve kümeler için](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="1c75f-162">Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **storm BASENAME** ve **kafka BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="1c75f-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="1c75f-163">Bu adları toohello kümeleri bağlanırken daha sonraki adımlarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c75f-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="1c75f-164">Merhaba kodu anlama</span><span class="sxs-lookup"><span data-stu-id="1c75f-164">Understanding hello code</span></span>

<span data-ttu-id="1c75f-165">Bu proje iki topoloji içerir:</span><span class="sxs-lookup"><span data-stu-id="1c75f-165">This project contains two topologies:</span></span>

* <span data-ttu-id="1c75f-166">**KafkaWriter**: hello tarafından tanımlanan **writer.yaml** dosyası, bu topoloji hello Apache Storm ile sağlanan KafkaBolt kullanarak rastgele cümleleri tooKafka yazar.</span><span class="sxs-lookup"><span data-stu-id="1c75f-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="1c75f-167">Bu topoloji bir özel kullanan **SentenceSpout** bileşen toogenerate rastgele cümleleri.</span><span class="sxs-lookup"><span data-stu-id="1c75f-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="1c75f-168">**KafkaReader**: hello tarafından tanımlanan **reader.yaml** dosyasını bu topoloji okur veriler Kafka hello Apache Storm ile sağlanan KafkaSpout kullanarak ve ardından günlükleri hello veri toostdout.</span><span class="sxs-lookup"><span data-stu-id="1c75f-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="1c75f-169">Bu topoloji hello Storm HdfsBolt toowrite veri toodefault depolama hello Storm kümesi için kullanır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="1c75f-170">Flux</span><span class="sxs-lookup"><span data-stu-id="1c75f-170">Flux</span></span>

<span data-ttu-id="1c75f-171">Merhaba topolojileri kullanılarak tanımlanır [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="1c75f-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="1c75f-172">Flux içinde sunulmuştur 0.10.x Storm ve tooseparate hello topoloji yapılandırması hello kodundan sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c75f-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="1c75f-173">Merhaba Flux framework kullanan topolojileri hello topoloji YAML dosyasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="1c75f-174">Merhaba YAML dosya hello topolojisinin bir parçası olarak dahil olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="1c75f-175">Ayrıca, hello topoloji gönderdiğinizde kullanılan tek başına dosya de olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="1c75f-176">Flux çalışma zamanında Bu örnekte kullanılan, değişkeni değiştirme de destekler.</span><span class="sxs-lookup"><span data-stu-id="1c75f-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="1c75f-177">Merhaba aşağıdaki parametreleri bu topolojiler için çalışma zamanında ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="1c75f-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="1c75f-178">`${kafka.topic}`: hello hello topolojileri okuma/yazma için Kafka konu hello adı.</span><span class="sxs-lookup"><span data-stu-id="1c75f-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="1c75f-179">`${kafka.broker.hosts}`: hello çalıştıracağınız Kafka aracıların bu hello barındırır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="1c75f-180">Merhaba aracısı bilgi KafkaBolt hello tarafından tooKafka yazılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="1c75f-181">`${kafka.zookeeper.hosts}`: Zookeeper çalışan üzerinde hello konakları hello Kafka küme.</span><span class="sxs-lookup"><span data-stu-id="1c75f-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="1c75f-182">Flux topolojileri hakkında daha fazla bilgi için bkz: [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="1c75f-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="1c75f-183">Karşıdan yükle ve Merhaba projeyi derleyin</span><span class="sxs-lookup"><span data-stu-id="1c75f-183">Download and compile hello project</span></span>

1. <span data-ttu-id="1c75f-184">Geliştirme ortamınızı hello projesinden indirmeniz [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), bir komut satırı açın ve dizinleri toohello konum hello proje indirdiğiniz değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="1c75f-185">Merhaba gelen **hdınsight storm java kafka** dizin kullanım hello aşağıdaki komut toocompile hello proje ve dağıtımı için bir paket oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1c75f-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="1c75f-186">Merhaba paket işlemi adlı bir dosya oluşturur `KafkaTopology-1.0-SNAPSHOT.jar` hello içinde `target` dizin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="1c75f-187">Komutları toocopy hello paket tooyour Storm Hdınsight kümesinde aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c75f-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="1c75f-188">Değiştir **kullanıcıadı** hello küme için hello SSH kullanıcı adı ile.</span><span class="sxs-lookup"><span data-stu-id="1c75f-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="1c75f-189">Değiştir **BASENAME** hello temel adıyla hello küme oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="1c75f-190">İstendiğinde, hello kümeleri oluşturulurken kullanılan hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="1c75f-191">Merhaba topolojisini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1c75f-191">Configure hello topology</span></span>

1. <span data-ttu-id="1c75f-192">Yöntemleri toodiscover aşağıdaki hello birini kullanın Kafka Aracısı konakları hello:</span><span class="sxs-lookup"><span data-stu-id="1c75f-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
    > <span data-ttu-id="1c75f-193">Merhaba Bash örnek varsayar `$CLUSTERNAME` hello Hdınsight kümesi hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="1c75f-194">Ayrıca varsayılmaktadır [jq](https://stedolan.github.io/jq/) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="1c75f-195">İstendiğinde, hello küme oturum açma hesabının hello parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="1c75f-196">döndürülen hello değeri metin aşağıdaki benzer toohello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1c75f-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="1c75f-197">Kümeniz için ikiden fazla Aracısı konakları olsa tooprovide tüm konaklar tooclients tam listesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1c75f-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="1c75f-198">Bir veya iki yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-198">One or two is enough.</span></span>

2. <span data-ttu-id="1c75f-199">Yöntemleri toodiscover hello Kafka Zookeeper konakları aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c75f-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
    > <span data-ttu-id="1c75f-200">Merhaba Bash örnek varsayar `$CLUSTERNAME` hello Hdınsight kümesi hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="1c75f-201">Ayrıca varsayılmaktadır [jq](https://stedolan.github.io/jq/) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="1c75f-202">İstendiğinde, hello küme oturum açma hesabının hello parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="1c75f-203">döndürülen hello değeri metin aşağıdaki benzer toohello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1c75f-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="1c75f-204">İkiden fazla Zookeeper düğümleri olsa da, tüm ana bilgisayarlar tooclients tam listesi tooprovide gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1c75f-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="1c75f-205">Bir veya iki yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-205">One or two is enough.</span></span>

    <span data-ttu-id="1c75f-206">Bu değer daha sonra kullanılmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="1c75f-207">Merhaba Düzenle `dev.properties` hello hello proje kökündeki dosyasında.</span><span class="sxs-lookup"><span data-stu-id="1c75f-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="1c75f-208">Bu dosyada Hello aracısı ve Zookeeper konakları bilgi toohello eşleşen satırları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="1c75f-209">Merhaba aşağıdaki örnek hello örnek değerler hello önceki adımları kullanarak yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="1c75f-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="1c75f-210">Merhaba Kaydet `dev.properties` dosya ve hello komut tooupload, toohello Storm kümesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c75f-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="1c75f-211">Değiştir **kullanıcıadı** hello küme için hello SSH kullanıcı adı ile.</span><span class="sxs-lookup"><span data-stu-id="1c75f-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="1c75f-212">Değiştir **BASENAME** hello temel adıyla hello küme oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="1c75f-213">Merhaba yazan Başlat</span><span class="sxs-lookup"><span data-stu-id="1c75f-213">Start hello writer</span></span>

1. <span data-ttu-id="1c75f-214">SSH kullanarak tooconnect toohello Storm kümesi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c75f-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="1c75f-215">Değiştir **kullanıcıadı** hello küme oluşturulurken kullanılan hello SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="1c75f-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="1c75f-216">Değiştir **BASENAME** hello küme oluşturulurken kullanılan hello temel ada sahip.</span><span class="sxs-lookup"><span data-stu-id="1c75f-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="1c75f-217">İstendiğinde, hello kümeleri oluşturulurken kullanılan hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="1c75f-218">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1c75f-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1c75f-219">SSH bağlantısı Hello komutu toocreate hello hello topolojisi tarafından kullanılan Kafka konu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c75f-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="1c75f-220">Değiştir `$KAFKAZKHOSTS` Zookeeper hello ile Merhaba önceki bölümde alınan bilgileri ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="1c75f-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="1c75f-221">Merhaba SSH bağlantı toohello Storm kümeden komutu toostart hello yazan topolojisi aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c75f-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="1c75f-222">Bu komutla birlikte kullanılan hello Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1c75f-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="1c75f-223">`org.apache.storm.flux.Flux`: Flux tooconfigure kullanın ve bu topoloji çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1c75f-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="1c75f-224">`--remote`: Hello topoloji tooNimbus gönderin.</span><span class="sxs-lookup"><span data-stu-id="1c75f-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="1c75f-225">Merhaba topoloji hello kümedeki hello çalışan düğümleri arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="1c75f-226">`-R /writer.yaml`: Kullanım Merhaba `writer.yaml` tooconfigure hello topoloji dosya.</span><span class="sxs-lookup"><span data-stu-id="1c75f-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="1c75f-227">`-R`Bu kaynak hello jar dosyasına dahil olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="1c75f-228">Bu nedenle hello jar hello kök dizininde olduğundan `/writer.yaml` hello yolu tooit olduğu.</span><span class="sxs-lookup"><span data-stu-id="1c75f-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="1c75f-229">`--filter`: Hello girdileri doldurmak `writer.yaml` hello değerleri kullanarak topolojisi `dev.properties` dosya.</span><span class="sxs-lookup"><span data-stu-id="1c75f-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="1c75f-230">Örneğin, hello değerini hello `kafka.topic` giriştir hello dosyasında kullanılan tooreplace hello `${kafka.topic}` hello topoloji tanımı girişi.</span><span class="sxs-lookup"><span data-stu-id="1c75f-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="1c75f-231">Merhaba topoloji başladıktan sonra veri toohello Kafka konu yazıyor komutu tooverify aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c75f-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="1c75f-232">Değiştir `$KAFKAZKHOSTS` Zookeeper hello ile Merhaba önceki bölümde alınan bilgileri ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="1c75f-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="1c75f-233">Bu komut, Kafka toomonitor hello konu ile birlikte gelen bir komut dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="1c75f-234">Bir süre sonra toohello konu yazılmış rastgele cümleleri döndürme başlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="1c75f-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="1c75f-235">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="1c75f-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="1c75f-236">Ctrl + c toostop hello komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c75f-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="1c75f-237">Merhaba reader'ı başlatın</span><span class="sxs-lookup"><span data-stu-id="1c75f-237">Start hello reader</span></span>

1. <span data-ttu-id="1c75f-238">Merhaba SSH oturumu toohello Storm kümeden komutu toostart hello okuyucu topolojisi aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c75f-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="1c75f-239">Merhaba topoloji başladıktan sonra hello Storm kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="1c75f-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="1c75f-240">Bu web kullanıcı Arabirimi https://storm-BASENAME.azurehdinsight.net/stormui bulunur.</span><span class="sxs-lookup"><span data-stu-id="1c75f-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="1c75f-241">Değiştir __BASENAME__ hello küme oluştururken kullandığınız hello temel adı ile.</span><span class="sxs-lookup"><span data-stu-id="1c75f-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="1c75f-242">İstendiğinde, hello yönetici oturum açma adı kullanın (varsayılan, `admin`) ve hello küme oluştururken kullanılan parola.</span><span class="sxs-lookup"><span data-stu-id="1c75f-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="1c75f-243">Görüntü izleyerek bir web sayfası benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="1c75f-243">You see a web page similar toohello following image:</span></span>

    ![Storm kullanıcı Arabirimi](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="1c75f-245">Storm kullanıcı Arabirimi Hello hello seçin __kafka okuyucu__ hello bağlantıyı __topoloji özeti__ bölümünde hello toodisplay bilgilerini __kafka okuyucu__ topolojisi.</span><span class="sxs-lookup"><span data-stu-id="1c75f-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Topoloji özeti kısmını hello Storm web kullanıcı Arabirimi](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="1c75f-247">Merhaba Günlükçü Cıvata bileşeninin select hello hello örnekleri hakkında toodisplay bilgi __Günlükçü Cıvata__ hello bağlantıyı __Cıvatalar (her zaman)__ bölümü.</span><span class="sxs-lookup"><span data-stu-id="1c75f-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Merhaba Cıvatalar bölümündeki Günlükçü Cıvata bağlantıyı](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="1c75f-249">Merhaba, __yürütücüler__ bölümünde, bir bağlantı hello seçin __bağlantı noktası__ hello bileşenin bu örneği hakkında sütun toodisplay günlük kaydı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1c75f-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Yürütücüler bağlantı](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="1c75f-251">Merhaba günlük hello Kafka konu ' okunan hello veri günlüğü içerir.</span><span class="sxs-lookup"><span data-stu-id="1c75f-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="1c75f-252">Merhaba günlüğünde Hello bilgi metnini izleyen benzer toohello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1c75f-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="1c75f-253">Merhaba topolojileri Durdur</span><span class="sxs-lookup"><span data-stu-id="1c75f-253">Stop hello topologies</span></span>

<span data-ttu-id="1c75f-254">Bir SSH oturumu toohello Storm kümeden komutları toostop hello Storm topolojilerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="1c75f-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="1c75f-255">Merhaba küme silme</span><span class="sxs-lookup"><span data-stu-id="1c75f-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="1c75f-256">Merhaba adımlar bu belgedeki her ikisi de oluşturma beri kümelerde Merhaba aynı Azure kaynak grubu, hello Azure portal hello kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c75f-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="1c75f-257">Bu belge aşağıdaki tarafından oluşturulan tüm kaynakları silme hello kaynak grubu kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1c75f-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c75f-258">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c75f-258">Next steps</span></span>

<span data-ttu-id="1c75f-259">Hdınsight üzerinde Storm ile kullanılan daha fazla örnek Topolojileri için bkz: [örnek Storm topolojileri ve bileşenleri](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="1c75f-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="1c75f-260">Dağıtma ve Linux tabanlı Hdınsight üzerinde topolojileri izleme hakkında daha fazla bilgi için bkz: [dağıtma ve Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1c75f-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>