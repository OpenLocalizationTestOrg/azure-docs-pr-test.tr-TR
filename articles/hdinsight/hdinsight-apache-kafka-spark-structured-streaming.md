---
title: "aaaApache Spark yapılandırılmış akış Kafka - Azure Hdınsight ile | Microsoft Docs"
description: "Bilgi nasıl toouse Apache Spark akış (DStream) tooget verilerini içine veya dışına Apache Kafka. Bu örnekte, Hdınsight'ta Spark gelen Jupyter Not Defteri kullanarak veri akışı."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="5beab-104">Hdınsight'ta Spark yapılandırılmış akış Kafka (Önizleme) ile kullanma</span><span class="sxs-lookup"><span data-stu-id="5beab-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="5beab-105">Bilgi nasıl toouse tooread verilerden Spark yapılandırılmış akış Azure hdınsight'ta Apache Kafka.</span><span class="sxs-lookup"><span data-stu-id="5beab-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="5beab-106">Yapılandırılmış Spark akış Spark SQL yerleşik bir akış işleme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="5beab-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="5beab-107">Bu, tooexpress akış hesaplamalar hello toplu hesaplama aynı statik verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5beab-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="5beab-108">Merhaba yapılandırılmış akışı hakkında daha fazla bilgi için bkz: [yapılandırılmış akış Programlama Kılavuzu [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) Apache.org.</span><span class="sxs-lookup"><span data-stu-id="5beab-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5beab-109">Bu örnek, Hdınsight 3.6 üzerinde Spark 2.1 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5beab-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="5beab-110">Yapılandırılmış akış olarak kabul __alfa__ Spark 2.1 üzerinde.</span><span class="sxs-lookup"><span data-stu-id="5beab-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="5beab-111">Bu belgedeki Hello adımlar hem hdınsight'ta Spark ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5beab-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="5beab-112">Bu kümeleri, hem bir Azure sanal hello Spark küme toodirectly sağlayan ağ içinde bulunan Kafka küme hello ile iletişim ' dir.</span><span class="sxs-lookup"><span data-stu-id="5beab-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="5beab-113">Bu belgedeki hello adımları tamamladığınızda, toodelete hello kümeleri tooavoid aşırı ücretleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5beab-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="5beab-114">Merhaba kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5beab-114">Create hello clusters</span></span>

<span data-ttu-id="5beab-115">Hdınsight üzerinde Apache Kafka sağlamaz erişim toohello Kafka aracıların üzerinden genel internet hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="5beab-116">Merhaba düğümler aynı Azure sanal ağ konuşmaları tooKafka olmalıdır hello herhangi bir şey Kafka küme hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="5beab-117">Bu örnekte, bir Azure sanal ağında hello Kafka ve Spark kümeleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="5beab-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="5beab-118">Merhaba Aşağıdaki diyagramda hello kümeleri arasında iletişimi nasıl akacağını gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5beab-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Bir Azure sanal ağı Spark ve Kafka kümelerde diyagramı](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="5beab-120">Merhaba Kafka hizmet hello sanal ağ içindeki sınırlı toocommunication ' dir.</span><span class="sxs-lookup"><span data-stu-id="5beab-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="5beab-121">Merhaba kümedeki diğer hizmetler gibi SSH ve Ambari, erişilebilir üzerinden internet hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="5beab-122">Merhaba ortak bağlantı noktaları Hdınsight ile kullanılabilir hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="5beab-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="5beab-123">Azure sanal ağı, Kafka ve Spark kümeleri el ile oluşturabileceğiniz olsa da, daha kolay toouse bir Azure Resource Manager şablonu durumdur.</span><span class="sxs-lookup"><span data-stu-id="5beab-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="5beab-124">Toodeploy Azure sanal ağı, Kafka, kullanım hello aşağıdaki adımları ve tooyour Azure aboneliği Spark kümeleri.</span><span class="sxs-lookup"><span data-stu-id="5beab-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="5beab-125">Düğme toosign tooAzure içinde ve açık hello şablonunda hello Azure portalı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="5beab-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="5beab-126">Hello Azure Resource Manager şablonu konumundadır **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="5beab-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="5beab-127">Bu şablon, kaynakları aşağıdaki hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="5beab-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="5beab-128">Hdınsight 3.5 kümede Kafka.</span><span class="sxs-lookup"><span data-stu-id="5beab-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="5beab-129">Bir Spark Hdınsight 3.6 kümede.</span><span class="sxs-lookup"><span data-stu-id="5beab-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="5beab-130">Bir Azure sanal hello Hdınsight kümeleri içeren ağ.</span><span class="sxs-lookup"><span data-stu-id="5beab-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5beab-131">Bu örnekte kullanılan hello yapılandırılmış akış not defteri Spark Hdınsight 3.6 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5beab-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="5beab-132">Hdınsight'ta Spark önceki bir sürümünü kullanıyorsanız, hello dizüstü bilgisayar kullanırken hataları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5beab-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="5beab-133">Bilgi toopopulate hello girişleri hello üzerinde aşağıdaki kullanım hello **özel dağıtım** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="5beab-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="5beab-135">**Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5beab-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="5beab-136">Bu grup hello Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="5beab-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="5beab-137">**Konum**: konum coğrafi olarak Kapat tooyou seçin.</span><span class="sxs-lookup"><span data-stu-id="5beab-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="5beab-138">**Temel küme adı**: Bu değer hello Spark ve Kafka kümelerinin hello temel adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5beab-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="5beab-139">Örneğin, **hdı** bir Spark spark hdi__ adlı Küme ve adlı bir Kafka kümesi oluşturur **kafka hdı**.</span><span class="sxs-lookup"><span data-stu-id="5beab-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="5beab-140">**Oturum açma kullanıcı adı küme**: hello Spark ve Kafka kümelerinin hello Yöneticisi kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="5beab-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="5beab-141">**Oturum açma parolası küme**: hello Spark ve Kafka kümeleri için hello yönetici kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="5beab-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="5beab-142">**SSH kullanıcı adı**: SSH kullanıcı toocreate hello Spark ve Kafka kümelerinin hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="5beab-143">**SSH parolası**: hello SSH kullanıcı hello Spark ve Kafka kümelerinin hello parolası.</span><span class="sxs-lookup"><span data-stu-id="5beab-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="5beab-144">Okuma hello **hüküm ve koşullar**ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.</span><span class="sxs-lookup"><span data-stu-id="5beab-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="5beab-145">Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="5beab-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="5beab-146">Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="5beab-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="5beab-147">Merhaba kaynakları oluşturduktan sonra yeniden yönlendirilen toohello kaynak grubu dikey demektir.</span><span class="sxs-lookup"><span data-stu-id="5beab-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Kaynak grubu dikey hello vnet ve kümeler için](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="5beab-149">Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **spark BASENAME** ve **kafka BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="5beab-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="5beab-150">Bu adları toohello kümeleri bağlanırken daha sonraki adımlarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="5beab-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="5beab-151">Aracıların Hello Kafka Al</span><span class="sxs-lookup"><span data-stu-id="5beab-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="5beab-152">Merhaba bu örnekteki kod bağlayan toohello Kafka Aracısı hello Kafka küme ana bilgisayarlar.</span><span class="sxs-lookup"><span data-stu-id="5beab-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="5beab-153">toofind Kafka Aracısı konakları Merhaba, aşağıdaki PowerShell veya Bash örneğine hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="5beab-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="5beab-154">Bu örnek bekliyor `$PASSWORD` toocontain hello hello küme oturum açma, parolasını ve `$CLUSTERNAME` toocontain hello hello Kafka küme adını.</span><span class="sxs-lookup"><span data-stu-id="5beab-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="5beab-155">Bu örnek hello kullanır [jq](https://stedolan.github.io/jq/) yardımcı programı tooparse veri hello JSON belgesi dışında.</span><span class="sxs-lookup"><span data-stu-id="5beab-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="5beab-156">Merhaba, benzer toohello metin aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="5beab-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="5beab-157">Aşağıdaki bölümlerde bu belgenin hello kullanılmak üzere bu bilgileri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5beab-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="5beab-158">Merhaba not defterlerini Al</span><span class="sxs-lookup"><span data-stu-id="5beab-158">Get hello notebooks</span></span>

<span data-ttu-id="5beab-159">Bu belgede açıklanan hello örneğin Hello kod şu adreste [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="5beab-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="5beab-160">Merhaba not defterlerini karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="5beab-160">Upload hello notebooks</span></span>

<span data-ttu-id="5beab-161">Adımları tooupload hello not defterlerini hello proje tooyour Spark Hdınsight kümesinde aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="5beab-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="5beab-162">Web tarayıcınızda toohello Jupyter Not Defteri, Spark kümesinde bağlayın.</span><span class="sxs-lookup"><span data-stu-id="5beab-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="5beab-163">URL, aşağıdaki Hello yerine `CLUSTERNAME` Kafka kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="5beab-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="5beab-164">İstendiğinde, hello küme oturum açma (Yönetici) ve hello küme oluştururken kullanılan parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="5beab-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="5beab-165">Merhaba Hello üst sağından hello sayfasında, kullanmak __karşıya__ düğmesini tooupload hello __akış Tweet'leri To_Kafka.ipynb__ dosya toohello kümesi.</span><span class="sxs-lookup"><span data-stu-id="5beab-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="5beab-166">Seçin __açık__ toostart hello karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="5beab-166">Select __Open__ toostart hello upload.</span></span>

    ![Merhaba karşıya yükleme düğmesini tooselect kullanın ve bir dizüstü bilgisayara yüklemek](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Merhaba KafkaStreaming.ipynb dosyasını seçin](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="5beab-169">Hello bulur __akış Tweet'leri To_Kafka.ipynb__ not defterlerini seçin ve hello listesi girişi __karşıya__ yanında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5beab-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Merhaba KafkaStreaming.ipynb girişi tooupload, toohello not defteri sunucu düğmesini kullanın hello karşıya yükleme](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="5beab-171">1-3 tooload hello arasındaki adımları yineleyin __Spark-yapılandırılmış-akış-gelen-Kafka.ipynb__ dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="5beab-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="5beab-172">Yük tweet'leri Kafka içine</span><span class="sxs-lookup"><span data-stu-id="5beab-172">Load tweets into Kafka</span></span>

<span data-ttu-id="5beab-173">Merhaba dosyaları karşıya sonra hello seçeneğini __akış Tweet'leri To_Kafka.ipynb__ girişi tooopen hello Not.</span><span class="sxs-lookup"><span data-stu-id="5beab-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="5beab-174">Kafka hello not defteri tooload tweet'leri Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5beab-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="5beab-175">İşlem tweet'leri Spark yapılandırılmış akış kullanma</span><span class="sxs-lookup"><span data-stu-id="5beab-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="5beab-176">Merhaba Hello ifadesini Jupyter not defteri giriş sayfası seçin __Spark-yapılandırılmış-akış-gelen-Kafka.ipynb__ girişi.</span><span class="sxs-lookup"><span data-stu-id="5beab-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="5beab-177">Spark yapılandırılmış akış kullanarak Kafka hello not defteri tooload tweet'leri Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5beab-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5beab-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5beab-178">Next steps</span></span>

<span data-ttu-id="5beab-179">Artık öğrendiğinize göre nasıl toouse Spark yapılandırılmış akış, belgeleri toolearn Spark ve Kafka ile çalışma hakkında daha fazla bilgi aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="5beab-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="5beab-180">[Nasıl toouse Spark Kafka ile akış (DStream)](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="5beab-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="5beab-181">Jupyter not defteri ve hdınsight'ta Spark ile Başlat</span><span class="sxs-lookup"><span data-stu-id="5beab-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)