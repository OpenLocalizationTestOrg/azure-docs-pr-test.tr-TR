---
title: "aaaCreate bir Apache Spark küme Azure Hdınsight'ta | Microsoft Docs"
description: "Hdınsight'ta bir Apache Spark toocreate küme nasıl üzerinde Hdınsight Spark hızlı başlangıç."
keywords: "spark hızlı başlangıç,etkileşimli spark,etkileşimli sorgu,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="5f43a-104">Azure HDInsight’ta Apache Spark kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f43a-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="5f43a-105">Bu makalede, nasıl toocreate bir Apache Spark küme Azure Hdınsight'ta öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="5f43a-106">HDInsight’ta Spark hakkında daha fazla bilgi için bkz. [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f43a-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="5f43a-107">![Azure Hdınsight'ta Apache Spark kümesi adımları toocreate açıklayan hızlı başlangıç diyagramı](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Hdınsight'ta Apache Spark kullanarak Spark hızlı başlangıç. Gösterilen adımlar: küme oluşturma; etkileşimli Spark sorgusu çalıştırma")</span><span class="sxs-lookup"><span data-stu-id="5f43a-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f43a-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5f43a-108">Prerequisites</span></span>

* <span data-ttu-id="5f43a-109">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="5f43a-109">**An Azure subscription**.</span></span> <span data-ttu-id="5f43a-110">Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f43a-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="5f43a-111">Bkz. [Ücretsiz Azure hesabınızı hemen oluşturun](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="5f43a-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="5f43a-112">HDInsight Spark kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f43a-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="5f43a-113">Bu bölümde, [Azure Resource Manager şablonu](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/) kullanarak bir HDInsight Spark kümesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5f43a-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="5f43a-114">Diğer küme oluşturma yöntemleri için bkz. [HDInsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5f43a-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="5f43a-115">Görüntü tooopen hello hello Azure portal şablonda aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5f43a-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="5f43a-116">Hello aşağıdaki değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="5f43a-116">Enter hello following values:</span></span>

    <span data-ttu-id="5f43a-117">![Azure Resource Manager şablonu kullanarak HDInsight Spark kümesi oluşturma](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Azure Resource Manager şablonu kullanarak Spark kümesi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="5f43a-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="5f43a-118">**Abonelik**: Bu kümeye ait Azure aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="5f43a-119">**Kaynak grubu**: Bir kaynak grubu oluşturun veya mevcut bir kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="5f43a-120">Kaynak grubu kullanılan toomanage olan projelerinizi için Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="5f43a-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="5f43a-121">**Konum**: hello kaynak grubu için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="5f43a-122">Merhaba şablon hello kümesi de hello varsayılan küme depolama ettirilmesi oluşturmak için bu konumu kullanır.</span><span class="sxs-lookup"><span data-stu-id="5f43a-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="5f43a-123">**ClusterName**: toocreate istediğiniz hello Hdınsight kümesi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="5f43a-124">**Spark sürüm**: seçin **2.0** tooinstall hello kümede istediğiniz hello sürüm olarak.</span><span class="sxs-lookup"><span data-stu-id="5f43a-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="5f43a-125">**Küme oturum açma adı ve parola**: hello varsayılan oturum açma adıdır, yönetici</span><span class="sxs-lookup"><span data-stu-id="5f43a-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="5f43a-126">**SSH kullanıcı adı ve parola**.</span><span class="sxs-lookup"><span data-stu-id="5f43a-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="5f43a-127">Bu değerleri not alın.</span><span class="sxs-lookup"><span data-stu-id="5f43a-127">Write down these values.</span></span>  <span data-ttu-id="5f43a-128">Bunları daha sonra hello öğreticide gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f43a-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="5f43a-129">Seçin **toohello hüküm ve koşullar yukarıda belirtildiği kabul**seçin **PIN toodashboard**ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="5f43a-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="5f43a-130">Şablon dağıtımı için Dağıtım gönderme başlıklı yeni bir kutucuk görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5f43a-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="5f43a-131">Yaklaşık 20 dakika toocreate hello küme alır.</span><span class="sxs-lookup"><span data-stu-id="5f43a-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="5f43a-132">Hdınsight kümeleri oluşturma konusunda bir sorun alıyorsanız, hello doğru izinleri toodo böylece yok olabilir.</span><span class="sxs-lookup"><span data-stu-id="5f43a-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="5f43a-133">Daha fazla bilgi için [erişim denetimi gereksinimlerine](hdinsight-administer-use-portal-linux.md#create-clusters) bakın.</span><span class="sxs-lookup"><span data-stu-id="5f43a-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="5f43a-134">Bu makalede kullanan bir Spark kümesi oluşturur [hello olarak Azure Storage Bloblarında küme depolama](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5f43a-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="5f43a-135">Kullanan bir Spark kümesi oluşturabilirsiniz [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) hello varsayılan depolama.</span><span class="sxs-lookup"><span data-stu-id="5f43a-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="5f43a-136">Yönergeler için bkz. [Data Lake Store ile HDInsight kümesi oluşturma](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5f43a-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="5f43a-137">Spark SQL kullanarak Hive sorgusu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5f43a-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="5f43a-138">Hdınsight Spark kümeniz için yapılandırılmış Jupyter not defteri kullandığınızda, bir hazır almak `sqlContext` Spark SQL kullanarak toorun Hive sorgularını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f43a-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="5f43a-139">Bu bölümde, bilgi nasıl toostart Jupyter not defteri ve temel Hive sorgusu çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="5f43a-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="5f43a-140">Açık hello [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5f43a-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="5f43a-141">Toopin hello küme toohello Pano ettiyseniz, hello Pano toolaunch hello küme dikey penceresinden hello küme kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f43a-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="5f43a-142">Merhaba sol bölmesinden hello küme toohello Pano değil sabitlerseniz tıklatın **Hdınsight kümeleri**ve ardından oluşturduğunuz hello kümesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f43a-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="5f43a-143">**Hızlı bağlantılar** bölümünde **Küme panoları**'na ve ardından **Jupyter Notebook**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f43a-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="5f43a-144">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="5f43a-145">![Açık Jupyter not defteri toorun etkileşimli Spark SQL sorgusu](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "açık Jupyter not defteri toorun etkileşimli Spark SQL sorgusu")</span><span class="sxs-lookup"><span data-stu-id="5f43a-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="5f43a-146">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f43a-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="5f43a-147">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="5f43a-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="5f43a-148">Bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f43a-148">Create a notebook.</span></span> <span data-ttu-id="5f43a-149">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f43a-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="5f43a-150">![Jupyter not defteri toorun etkileşimli Spark SQL sorgu oluşturma](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter not defteri toorun etkileşimli Spark SQL sorgu oluşturma")</span><span class="sxs-lookup"><span data-stu-id="5f43a-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="5f43a-151">Yeni bir not defteri oluşturulur ve Untitled(Untitled.pynb) hello adı ile açılır.</span><span class="sxs-lookup"><span data-stu-id="5f43a-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="5f43a-152">Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve isterseniz kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="5f43a-153">![Merhaba Jupter not defteri toorun etkileşimli Spark sorgu için bir ad](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "hello Jupter not defteri toorun etkileşimli Spark sorgu için bir ad sağlayın")</span><span class="sxs-lookup"><span data-stu-id="5f43a-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="5f43a-154">Yapıştır hello aşağıdaki kod boş bir hücreye ve tuşuna basarak **SHIFT + ENTER** toorun hello kodu.</span><span class="sxs-lookup"><span data-stu-id="5f43a-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="5f43a-155">Aşağıdaki hello kodda `%%sql` (çağrılan hello sql Sihirli) söyler Jupyter not defteri toouse hello önceden `sqlContext` toorun hello Hive sorgusu.</span><span class="sxs-lookup"><span data-stu-id="5f43a-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="5f43a-156">Merhaba sorgu hello üst 10 satır Hive tablosundan alır (**hivesampletable**) tüm Hdınsight kümeleri üzerinde varsayılan olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5f43a-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="5f43a-157">![HDInsight Spark'ta Hive sorgusu](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "HDInsight Spark'ta Hive sorgusu")</span><span class="sxs-lookup"><span data-stu-id="5f43a-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="5f43a-158">Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli ve hello önceden bağlamları bkz [Jupyter defterlerinde Hdınsight kümesi için kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="5f43a-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f43a-159">Jupyter'de bir sorgu çalıştırmadan her zaman, web tarayıcınızın Pencere başlığında gösteren bir **(meşgul)** hello not defteri başlığı ile birlikte durum.</span><span class="sxs-lookup"><span data-stu-id="5f43a-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="5f43a-160">Ayrıca dolu daire sonraki toohello bkz **PySpark** hello sağ üst köşedeki metin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="5f43a-161">Merhaba iş tamamlandıktan sonra tooa boş daire değiştirir.</span><span class="sxs-lookup"><span data-stu-id="5f43a-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="5f43a-162">Merhaba ekranında tooshow hello sorgu çıktısı yenilemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f43a-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="5f43a-163">![HDInsight Spark'ta Hive sorgusu çıkışı](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "HDInsight Spark'ta Hive sorgusu çıkışı")</span><span class="sxs-lookup"><span data-stu-id="5f43a-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="5f43a-164">Merhaba uygulaması çalıştıran bitirdikten sonra hello not defteri toorelease hello küme kaynaklarını kapatın.</span><span class="sxs-lookup"><span data-stu-id="5f43a-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="5f43a-165">toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.</span><span class="sxs-lookup"><span data-stu-id="5f43a-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="5f43a-166">Daha sonraki bir zamanda toocomplete hello sonraki adımlar planlıyorsanız, bu makaledeki oluşturulan hello Hdınsight kümesi silme emin olun.</span><span class="sxs-lookup"><span data-stu-id="5f43a-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="5f43a-167">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="5f43a-167">Next step</span></span> 

<span data-ttu-id="5f43a-168">Sorgu öğrenilen nasıl toocreate bir Hdınsight Spark küme bu makalede ve temel bir Spark SQL Çalıştır.</span><span class="sxs-lookup"><span data-stu-id="5f43a-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="5f43a-169">Toohello nasıl toouse bir Hdınsight Spark küme sonraki makalede toolearn toorun etkileşimli sorgular örnek verilere ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="5f43a-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="5f43a-170">Bir HDInsight Spark kümesinde etkileşimli sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5f43a-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



