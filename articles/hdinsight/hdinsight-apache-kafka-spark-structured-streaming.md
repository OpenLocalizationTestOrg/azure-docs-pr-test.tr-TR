---
title: "Apache Spark yapılandırılmış Kafka - Azure Hdınsight akış | Microsoft Docs"
description: "Apache Spark (DStream) akış içine veya dışına Apache Kafka veri almak için nasıl kullanılacağını öğrenin. Bu örnekte, Hdınsight'ta Spark gelen Jupyter Not Defteri kullanarak veri akışı."
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
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="245cf-104">Hdınsight'ta Spark yapılandırılmış akış Kafka (Önizleme) ile kullanma</span><span class="sxs-lookup"><span data-stu-id="245cf-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="245cf-105">Spark yapılandırılmış akış verilerini Azure hdınsight'ta Apache Kafka okumak için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="245cf-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="245cf-106">Yapılandırılmış Spark akış Spark SQL yerleşik bir akış işleme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="245cf-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="245cf-107">Akış hesaplamalar express için toplu hesaplama aynı statik verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="245cf-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="245cf-108">Yapılandırılmış akışı hakkında daha fazla bilgi için bkz: [yapılandırılmış akış Programlama Kılavuzu [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) Apache.org.</span><span class="sxs-lookup"><span data-stu-id="245cf-108">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="245cf-109">Bu örnek, Hdınsight 3.6 üzerinde Spark 2.1 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="245cf-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="245cf-110">Yapılandırılmış akış olarak kabul __alfa__ Spark 2.1 üzerinde.</span><span class="sxs-lookup"><span data-stu-id="245cf-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="245cf-111">Bu belgede yer alan adımlar, hem hdınsight'ta Spark ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="245cf-111">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="245cf-112">Bu kümeleri, hem bir Azure sanal Kafka ile doğrudan iletişim kurmak Spark kümesi sağlayan ağ içinde bulunan küme ' dir.</span><span class="sxs-lookup"><span data-stu-id="245cf-112">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="245cf-113">Bu belgedeki adımları tamamladığınızda, aşırı ücretlerden kaçınmak için kümelerini Sil unutmayın.</span><span class="sxs-lookup"><span data-stu-id="245cf-113">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="245cf-114">Kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="245cf-114">Create the clusters</span></span>

<span data-ttu-id="245cf-115">Hdınsight üzerinde Apache Kafka erişim genel internet üzerinden Kafka aracıların sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="245cf-115">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="245cf-116">İçin Kafka ettiği herhangi bir şey Kafka kümedeki düğümlerin aynı Azure sanal ağ içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="245cf-116">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="245cf-117">Bu örnekte, bir Azure sanal ağında Kafka ve Spark kümeleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="245cf-117">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="245cf-118">Aşağıdaki diyagramda, iletişim kümeleri arasında nasıl aktığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="245cf-118">The following diagram shows how communication flows between the clusters:</span></span>

![Bir Azure sanal ağı Spark ve Kafka kümelerde diyagramı](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="245cf-120">Sanal ağ içinde iletişimi Kafka hizmet sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="245cf-120">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="245cf-121">Kümedeki SSH ve Ambari, gibi diğer hizmetlerin internet üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="245cf-121">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="245cf-122">Hdınsight ile kullanılabilen ortak bağlantı noktaları hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="245cf-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="245cf-123">Azure sanal ağı, Kafka, oluşturabilir ve el ile Spark kümeleri olsa da, bir Azure Resource Manager şablonunu kullanmak daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="245cf-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="245cf-124">Azure sanal ağı, Kafka, dağıtmak ve Spark kümeleri Azure aboneliğiniz için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="245cf-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="245cf-125">Azure'da oturum açın ve Azure portalında şablon açmak için aşağıdaki düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="245cf-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="245cf-126">Azure Resource Manager şablonu bulunur **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="245cf-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="245cf-127">Bu şablon, aşağıdaki kaynaklara oluşturur:</span><span class="sxs-lookup"><span data-stu-id="245cf-127">This template creates the following resources:</span></span>

    * <span data-ttu-id="245cf-128">Hdınsight 3.5 kümede Kafka.</span><span class="sxs-lookup"><span data-stu-id="245cf-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="245cf-129">Bir Spark Hdınsight 3.6 kümede.</span><span class="sxs-lookup"><span data-stu-id="245cf-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="245cf-130">Bir Azure sanal Hdınsight kümeleri içeren ağ.</span><span class="sxs-lookup"><span data-stu-id="245cf-130">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="245cf-131">Bu örnekte kullanılan yapılandırılmış akış dizüstü Spark Hdınsight 3.6 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="245cf-131">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="245cf-132">Hdınsight'ta Spark önceki bir sürümünü kullanıyorsanız, dizüstü bilgisayar kullanırken hataları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="245cf-132">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="245cf-133">Üzerinde girişleri doldurmak için aşağıdaki bilgileri kullanın **özel dağıtım** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="245cf-133">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="245cf-135">**Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="245cf-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="245cf-136">Bu grup, Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="245cf-136">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="245cf-137">**Konum**: coğrafi olarak yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="245cf-137">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="245cf-138">**Temel küme adı**: Bu değer Spark temel adı olarak kullanılır ve Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="245cf-138">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="245cf-139">Örneğin, **hdı** bir Spark spark hdi__ adlı Küme ve adlı bir Kafka kümesi oluşturur **kafka hdı**.</span><span class="sxs-lookup"><span data-stu-id="245cf-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="245cf-140">**Oturum açma kullanıcı adı küme**: Spark ve Kafka kümeleri için yönetici kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="245cf-140">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="245cf-141">**Oturum açma parolası küme**: Spark ve Kafka kümeleri için yönetici kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="245cf-141">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="245cf-142">**SSH kullanıcı adı**: için Spark ve Kafka kümeleri oluşturmak için SSH kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="245cf-142">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="245cf-143">**SSH parolası**: Spark ve Kafka kümelerinin SSH kullanıcısının parolası.</span><span class="sxs-lookup"><span data-stu-id="245cf-143">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="245cf-144">Okuma **hüküm ve koşullar**ve ardından **hüküm ve koşulları yukarıda belirtildiği ediyorum**.</span><span class="sxs-lookup"><span data-stu-id="245cf-144">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="245cf-145">Son olarak, denetleme **panoya Sabitle** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="245cf-145">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="245cf-146">Kümeleri oluşturmak için yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="245cf-146">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="245cf-147">Kaynakları oluşturduktan sonra kaynak grubu dikey penceresine yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="245cf-147">Once the resources have been created, you are redirected to the resource group blade.</span></span>

![Kaynak grubu dikey vnet ve kümeler için](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="245cf-149">Hdınsight kümeleri adlarının bildirimi **spark BASENAME** ve **kafka BASENAME**, BASENAME şablona verdiğiniz adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="245cf-149">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="245cf-150">Kümeye bağlanırken bu adları daha sonraki adımlarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="245cf-150">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="245cf-151">Aracıların Kafka Al</span><span class="sxs-lookup"><span data-stu-id="245cf-151">Get the Kafka brokers</span></span>

<span data-ttu-id="245cf-152">Bu örnekteki kod Kafka kümedeki Kafka Aracısı ana bağlanır.</span><span class="sxs-lookup"><span data-stu-id="245cf-152">The code in this example connects to the Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="245cf-153">Kafka Aracısı ana bilgisayarları bulmak için aşağıdaki PowerShell veya Bash örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="245cf-153">To find the Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
> <span data-ttu-id="245cf-154">Bu örnek bekliyor `$PASSWORD` küme oturum açma için parola içerecek şekilde ve `$CLUSTERNAME` Kafka küme adı içeriyor.</span><span class="sxs-lookup"><span data-stu-id="245cf-154">This example expects `$PASSWORD` to contain the password for the cluster login, and `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="245cf-155">Bu örnekte [jq](https://stedolan.github.io/jq/) JSON belgesini dışında verileri ayrıştırmak için yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="245cf-155">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

<span data-ttu-id="245cf-156">Çıktı aşağıdaki metne benzer:</span><span class="sxs-lookup"><span data-stu-id="245cf-156">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="245cf-157">Bu belge aşağıdaki bölümlerde kullanılmak üzere bu bilgileri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="245cf-157">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="245cf-158">Not defterlerini Al</span><span class="sxs-lookup"><span data-stu-id="245cf-158">Get the notebooks</span></span>

<span data-ttu-id="245cf-159">Bu belgede açıklanan örnek kodunu şu adresten edinilebilir [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="245cf-159">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="245cf-160">Not defterlerini karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="245cf-160">Upload the notebooks</span></span>

<span data-ttu-id="245cf-161">Proje defterlerinden, Spark Hdınsight kümesinde için karşıya yüklemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="245cf-161">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="245cf-162">Web tarayıcınız, Spark kümesinde Jupyter not defteri bağlayın.</span><span class="sxs-lookup"><span data-stu-id="245cf-162">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="245cf-163">Aşağıdaki URL ile değiştirin `CLUSTERNAME` Kafka kümenizin adıyla:</span><span class="sxs-lookup"><span data-stu-id="245cf-163">In the following URL, replace `CLUSTERNAME` with the name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="245cf-164">İstendiğinde, küme oturum açma (Yönetici) ve küme oluştururken kullanılan parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="245cf-164">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="245cf-165">Sayfanın üst sağ taraftan kullanmak __karşıya__ karşıya yüklemek için düğmeyi __akış Tweet'leri To_Kafka.ipynb__ kümeye dosya.</span><span class="sxs-lookup"><span data-stu-id="245cf-165">From the upper right side of the page, use the __Upload__ button to upload the __Stream-Tweets-To_Kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="245cf-166">Seçin __açık__ başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="245cf-166">Select __Open__ to start the upload.</span></span>

    ![Karşıya yükleme düğmesini seçin ve bir dizüstü bilgisayara yüklemek için kullanın](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![KafkaStreaming.ipynb dosyasını seçin](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="245cf-169">Bul __akış Tweet'leri To_Kafka.ipynb__ not defterlerini ve select listesi girişi __karşıya__ yanında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="245cf-169">Find the __Stream-Tweets-To_Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Not Defteri sunucuya yüklemek için KafkaStreaming.ipynb girişi yanındaki karşıya yükleme düğmesini kullanın](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="245cf-171">Yüklemek için 1-3 arasındaki adımları yineleyin __Spark-yapılandırılmış-akış-gelen-Kafka.ipynb__ dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="245cf-171">Repeat steps 1-3 to load the __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="245cf-172">Yük tweet'leri Kafka içine</span><span class="sxs-lookup"><span data-stu-id="245cf-172">Load tweets into Kafka</span></span>

<span data-ttu-id="245cf-173">Karşıya yüklenen dosyaların sonra seçeneğini __akış Tweet'leri To_Kafka.ipynb__ girişi not defterini açın.</span><span class="sxs-lookup"><span data-stu-id="245cf-173">Once the files have been uploaded, select the __Stream-Tweets-To_Kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="245cf-174">Tweet'leri Kafka yüklemek için Not Defteri'ndaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="245cf-174">Follow the steps in the notebook to load tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="245cf-175">İşlem tweet'leri Spark yapılandırılmış akış kullanma</span><span class="sxs-lookup"><span data-stu-id="245cf-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="245cf-176">Jupyter not defteri giriş sayfadan seçin __Spark-yapılandırılmış-akış-gelen-Kafka.ipynb__ girişi.</span><span class="sxs-lookup"><span data-stu-id="245cf-176">From the Jupyter Notebook home page, select the __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="245cf-177">Tweet'leri Kafka Spark yapılandırılmış akış kullanarak yüklemek için not defterindeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="245cf-177">Follow the steps in the notebook to load tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="245cf-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="245cf-178">Next steps</span></span>

<span data-ttu-id="245cf-179">Spark yapılandırılmış akış kullanmayı öğrendiniz, Spark ve Kafka ile çalışma hakkında daha fazla bilgi için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="245cf-179">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="245cf-180">[(DStream) ile Kafka Spark akış kullanmayı](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="245cf-180">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="245cf-181">Jupyter not defteri ve hdınsight'ta Spark ile Başlat</span><span class="sxs-lookup"><span data-stu-id="245cf-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)