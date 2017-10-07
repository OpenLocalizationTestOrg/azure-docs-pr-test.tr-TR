---
title: "Azure hdınsight'ta Spark Jupyter'de aaaUse özel Maven paketleri | Microsoft Docs"
description: "Nasıl tooconfigure Jupyter not defterleri ile Hdınsight Spark kullanılabilir kümeleri toouse özel Maven paketleri ilişkin adım adım yönergeler için."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="8a14a-103">Hdınsight'ta Apache Spark kümeleri Jupyter not defterlerinde ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a14a-104">Hücre Sihirli kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="8a14a-105">Betik eylemi kullanarak</span><span class="sxs-lookup"><span data-stu-id="8a14a-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="8a14a-106">Nasıl tooconfigure Hdınsight toouse dış, Apache Spark kümesinde Jupyter not defteri topluluk-katkıda öğrenin **maven** hello kümede olmayan paketler dahil Giden kutusu.</span><span class="sxs-lookup"><span data-stu-id="8a14a-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="8a14a-107">Merhaba arayabilirsiniz [Maven depo](http://search.maven.org/) hello tam kullanılabilir paketler listesi.</span><span class="sxs-lookup"><span data-stu-id="8a14a-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="8a14a-108">Ayrıca, diğer kaynaklardan kullanılabilir paketlerin listesini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a14a-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="8a14a-109">Örneğin, tamamını topluluk katkıda bulunan paketlerin listesini adresten edinilebilir [Spark paketleri](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="8a14a-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="8a14a-110">Bu makalede, öğreneceksiniz nasıl toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) hello Jupyter not defteri paketiyle.</span><span class="sxs-lookup"><span data-stu-id="8a14a-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="8a14a-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8a14a-111">Prerequisites</span></span>
<span data-ttu-id="8a14a-112">Merhaba şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a14a-112">You must have hello following:</span></span>

* <span data-ttu-id="8a14a-113">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="8a14a-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8a14a-114">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8a14a-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="8a14a-115">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="8a14a-116">Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a14a-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="8a14a-117">Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="8a14a-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="8a14a-118">Merhaba Spark kümesi dikey penceresinden tıklatın **hızlı bağlantılar**ve sonra hello **küme Panosu** dikey penceresinde tıklatın **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="8a14a-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="8a14a-119">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="8a14a-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a14a-120">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="8a14a-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="8a14a-121">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="8a14a-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="8a14a-122">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a14a-122">Create a new notebook.</span></span> <span data-ttu-id="8a14a-123">Tıklatın **yeni**ve ardından **Spark**.</span><span class="sxs-lookup"><span data-stu-id="8a14a-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="8a14a-124">![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Yeni bir Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="8a14a-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="8a14a-125">Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile.</span><span class="sxs-lookup"><span data-stu-id="8a14a-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="8a14a-126">Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8a14a-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="8a14a-127">![Merhaba dizüstü bilgisayar için bir ad](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "hello dizüstü bilgisayar için bir ad sağlayın")</span><span class="sxs-lookup"><span data-stu-id="8a14a-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="8a14a-128">Merhaba kullanacağınız `%%configure` Sihirli tooconfigure hello not defteri toouse bir dış paketi.</span><span class="sxs-lookup"><span data-stu-id="8a14a-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="8a14a-129">Dış paketleri kullanma defterlerinde hello çağrı emin olun `%%configure` hello birinci kod hücresini Sihirli.</span><span class="sxs-lookup"><span data-stu-id="8a14a-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="8a14a-130">Bu hello oturum başlamadan önce bu hello çekirdek yapılandırılmış toouse hello paketi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a14a-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="8a14a-131">Merhaba ilk hücresinde tooconfigure hello çekirdek unutursanız, hello kullanabilirsiniz `%%configure` hello ile `-f` parametre ancak hello oturumu başlatacak ve tüm ilerleme kaybolacak.</span><span class="sxs-lookup"><span data-stu-id="8a14a-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="8a14a-132">Hdınsight sürümü</span><span class="sxs-lookup"><span data-stu-id="8a14a-132">HDInsight version</span></span> | <span data-ttu-id="8a14a-133">Komut</span><span class="sxs-lookup"><span data-stu-id="8a14a-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="8a14a-134">Hdınsight 3.3 ve Hdınsight 3.4</span><span class="sxs-lookup"><span data-stu-id="8a14a-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="8a14a-135">Hdınsight 3.5</span><span class="sxs-lookup"><span data-stu-id="8a14a-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="8a14a-136">Yukarıdaki Hello parçacığında hello maven koordinatları hello dış Maven merkezi bir depoya paketinde için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8a14a-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="8a14a-137">Bu parçacığında bulunan `com.databricks:spark-csv_2.10:1.4.0` hello maven koordinatı olan **spark csv** paket.</span><span class="sxs-lookup"><span data-stu-id="8a14a-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="8a14a-138">İşte nasıl hello koordinatları bir paket için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a14a-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="8a14a-139">a.</span><span class="sxs-lookup"><span data-stu-id="8a14a-139">a.</span></span> <span data-ttu-id="8a14a-140">Merhaba paketi hello Maven depo bulun.</span><span class="sxs-lookup"><span data-stu-id="8a14a-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="8a14a-141">Bu öğretici için kullandığımız [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="8a14a-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="8a14a-142">b.</span><span class="sxs-lookup"><span data-stu-id="8a14a-142">b.</span></span> <span data-ttu-id="8a14a-143">Merhaba depodan hello değerlerini toplamak **GroupID**, **Artifactıd**, ve **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="8a14a-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="8a14a-144">Merhaba değerleri toplamanız kümenizi eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="8a14a-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="8a14a-145">Bu durumda, Scala 2.10 ve Spark 1.4.0 paket kullanıyoruz, ancak kümenizdeki hello için uygun Scala veya Spark sürüm tooselect farklı sürümlerini gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8a14a-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="8a14a-146">Merhaba Scala sürümü kümenizde çalıştırarak bulabileceğiniz `scala.util.Properties.versionString` hello Spark Jupyter çekirdek veya Spark Gönder.</span><span class="sxs-lookup"><span data-stu-id="8a14a-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="8a14a-147">Hello Spark sürüm kümenizde çalıştırarak bulabileceğiniz `sc.version` Jupyter Not.</span><span class="sxs-lookup"><span data-stu-id="8a14a-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="8a14a-148">![Jupyter not defteri ile dış paketleri kullanma](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Jupyter not defteri ile dış paketleri kullanma")</span><span class="sxs-lookup"><span data-stu-id="8a14a-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="8a14a-149">c.</span><span class="sxs-lookup"><span data-stu-id="8a14a-149">c.</span></span> <span data-ttu-id="8a14a-150">Merhaba üç değerleri, virgülle ayrılmış birleştirme (**:**).</span><span class="sxs-lookup"><span data-stu-id="8a14a-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="8a14a-151">Merhaba kod hücre ile Merhaba çalıştırmak `%%configure` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="8a14a-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="8a14a-152">Bu, sağladığınız hello temel Livy oturum toouse hello paket yapılandıracak.</span><span class="sxs-lookup"><span data-stu-id="8a14a-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="8a14a-153">Merhaba sonraki hücrelerde hello not defterinde, aşağıda gösterildiği gibi hello paket artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a14a-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="8a14a-154">Merhaba parçacıkları sonra çalıştırabilir, aşağıda gösterilen tooview gibi hello hello dataframe verilerden hello önceki adımda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="8a14a-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="8a14a-155"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8a14a-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8a14a-156">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="8a14a-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8a14a-157">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="8a14a-157">Scenarios</span></span>
* [<span data-ttu-id="8a14a-158">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="8a14a-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8a14a-159">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8a14a-160">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8a14a-161">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="8a14a-162">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="8a14a-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8a14a-163">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8a14a-163">Create and run applications</span></span>
* [<span data-ttu-id="8a14a-164">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a14a-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8a14a-165">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8a14a-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8a14a-166">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="8a14a-166">Tools and extensions</span></span>

* [<span data-ttu-id="8a14a-167">Hdınsight Linux üzerinde Apache Spark kümeleri Jupyter not defterlerinde ile dış python paketlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="8a14a-168">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="8a14a-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8a14a-169">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8a14a-170">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="8a14a-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8a14a-171">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="8a14a-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8a14a-172">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="8a14a-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8a14a-173">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="8a14a-173">Manage resources</span></span>
* [<span data-ttu-id="8a14a-174">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8a14a-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8a14a-175">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="8a14a-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

