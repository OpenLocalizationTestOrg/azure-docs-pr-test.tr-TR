---
title: "Microsoft Azure Hdınsight Spark derin öğrenme için ile Bilişsel Araç Seti | Microsoft Docs"
description: "Bir Azure Hdınsight Spark kümesinde Spark Python API kullanarak bir veri kümesi Microsoft Bilişsel Araç Seti derin learning modeli nasıl uygulanabilir öğrenin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: fafd738f782660b824732bab8cc3bec8405947e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="cb990-103">Microsoft Azure Hdınsight Spark küme modeliyle öğrenme derin bir Bilişsel araç kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="cb990-104">Bu makalede, aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="cb990-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="cb990-105">Bir Azure Hdınsight Spark kümesinde Microsoft Bilişsel Araç Seti yüklemek için özel bir komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cb990-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="cb990-106">Bir Azure Blob Depolama hesabı kullanarak dosyaları Microsoft Bilişsel Araç Seti derin learning modeli uygulamak nasıl görmek için Spark kümesi Jupyter not defteri karşıya [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="cb990-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb990-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cb990-107">Prerequisites</span></span>

* <span data-ttu-id="cb990-108">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="cb990-108">**An Azure subscription**.</span></span> <span data-ttu-id="cb990-109">Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb990-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="cb990-110">Bkz. [Ücretsiz Azure hesabınızı hemen oluşturun](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="cb990-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="cb990-111">**Azure Hdınsight Spark kümesi**.</span><span class="sxs-lookup"><span data-stu-id="cb990-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="cb990-112">Bu makalede, bir Spark 2.0 kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cb990-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="cb990-113">Yönergeler için bkz: [Azure hdınsight'ta Apache Spark oluşturma küme](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cb990-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="cb990-114">Bu çözümün nasıl akıyor?</span><span class="sxs-lookup"><span data-stu-id="cb990-114">How does this solution flow?</span></span>

<span data-ttu-id="cb990-115">Bu çözüm, bu makalede ve bu öğreticinin bir parçası olarak karşıya Jupyter not defteri arasında bölünür.</span><span class="sxs-lookup"><span data-stu-id="cb990-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="cb990-116">Bu makalede, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="cb990-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="cb990-117">Betik eylemi Microsoft Bilişsel Araç Seti ve Python paketlerini yüklemek için bir Hdınsight Spark kümesinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cb990-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="cb990-118">Hdınsight Spark kümesi çözümü çalıştıran Jupyter not defteri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cb990-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="cb990-119">Aşağıdaki adımları Jupyter not defteri ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="cb990-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="cb990-120">Yük örnek görüntülere Spark Resiliant dağıtılmış Dataset ya da RDD</span><span class="sxs-lookup"><span data-stu-id="cb990-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="cb990-121">Modülleri yüklemek ve hazır tanımlayın</span><span class="sxs-lookup"><span data-stu-id="cb990-121">Load modules and define presets</span></span>
   - <span data-ttu-id="cb990-122">Veri kümesi Spark küme üzerinde yerel olarak indir</span><span class="sxs-lookup"><span data-stu-id="cb990-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="cb990-123">Veri kümesi bir RDD Dönüştür</span><span class="sxs-lookup"><span data-stu-id="cb990-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="cb990-124">Bilişsel Araç Seti modeli kullanarak görüntüleri puan</span><span class="sxs-lookup"><span data-stu-id="cb990-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="cb990-125">Spark kümesi eğitim Bilişsel Araç Seti modeli indirme</span><span class="sxs-lookup"><span data-stu-id="cb990-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="cb990-126">Alt düğümler tarafından kullanılacak işlevleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="cb990-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="cb990-127">Görüntüleri çalışan düğümlerine puan</span><span class="sxs-lookup"><span data-stu-id="cb990-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="cb990-128">Model doğruluğundan değerlendir</span><span class="sxs-lookup"><span data-stu-id="cb990-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="cb990-129">Microsoft Bilişsel Araç Seti yükleyin</span><span class="sxs-lookup"><span data-stu-id="cb990-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="cb990-130">Betik eylemi kullanarak Spark kümesinde Microsoft Bilişsel Araç Seti yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb990-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="cb990-131">Betik eylemi özel komut dosyaları varsayılan olarak kullanılabilir değil küme üzerinde bileşenleri yüklemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="cb990-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="cb990-132">Hdınsight .NET SDK kullanarak ya da Azure PowerShell kullanarak Azure portalından özel komut dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb990-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="cb990-133">Araç Seti ya da küme oluşturma veya kümeye çalışır durumda sonra bir parçası olarak yüklemek için komut dosyasını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb990-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="cb990-134">Bu makalede, Küme oluşturulduktan sonra araç seti yüklemek için Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb990-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="cb990-135">Özel komut dosyasını çalıştırmak diğer yolları için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cb990-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="cb990-136">Azure Portal’ı kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-136">Using the Azure Portal</span></span>

<span data-ttu-id="cb990-137">Betik eylemi çalıştırmak için Azure Portalı'nı kullanma hakkında daha fazla yönerge için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="cb990-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="cb990-138">Microsoft Bilişsel Araç Seti yüklemek için aşağıdaki girişleri sağladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cb990-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="cb990-139">Betik eylem adı için bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="cb990-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="cb990-140">İçin **betik URI Bash**, girin `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="cb990-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="cb990-141">Yalnızca head ve çalışan düğümlerine komut dosyasını çalıştırın ve tüm diğer onay kutularını temizleyin emin olun.</span><span class="sxs-lookup"><span data-stu-id="cb990-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="cb990-142">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb990-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="cb990-143">Azure Hdınsight Spark kümesinde Jupyter not defteri karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="cb990-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="cb990-144">Microsoft Bilişsel araç seti ile Azure Hdınsight Spark kümesi kullanmak üzere Jupyter not defteri yük **CNTK_model_scoring_on_Spark_walkthrough.ipynb** Azure Hdınsight Spark küme.</span><span class="sxs-lookup"><span data-stu-id="cb990-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="cb990-145">Bu not defteri github'da kullanılabilir [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="cb990-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="cb990-146">GitHub deposunu kopyalayın [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="cb990-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="cb990-147">Kopyalamak yönergeler için bkz: [depo kopyalama](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="cb990-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="cb990-148">Azure Portalı'ndan zaten sağlanmış tıklatın Spark kümesi dikey penceresini açmak **küme Panosu**ve ardından **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="cb990-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="cb990-149">URL'sine giderek Jupyter not defteri başlatabilirsiniz `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="cb990-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="cb990-150">Değiştir \<clustername > Hdınsight kümenize adı.</span><span class="sxs-lookup"><span data-stu-id="cb990-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="cb990-151">Jupyter not defteri tıklatın **karşıya** içinde sağ üst köşe ve GitHub deposunu kopyaladığınız konuma gidin.</span><span class="sxs-lookup"><span data-stu-id="cb990-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="cb990-152">![Azure Hdınsight Spark kümesinde Jupyter not defteri karşıya](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Azure Hdınsight Spark kümesi için karşıya yükleme Jupyter not defteri")</span><span class="sxs-lookup"><span data-stu-id="cb990-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="cb990-153">Tıklatın **karşıya** yeniden.</span><span class="sxs-lookup"><span data-stu-id="cb990-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="cb990-154">Not Defteri karşıya yüklendikten sonra dizüstü bilgisayar adına tıklayın ve veri kümesi yükleme ve öğreticiyi gerçekleştirme hakkında dizüstü kendisini'ndaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="cb990-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="cb990-155">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="cb990-155">See also</span></span>
* [<span data-ttu-id="cb990-156">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="cb990-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="cb990-157">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="cb990-157">Scenarios</span></span>
* [<span data-ttu-id="cb990-158">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="cb990-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="cb990-159">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="cb990-160">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="cb990-161">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="cb990-162">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="cb990-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="cb990-163">HDInsight’ta Spark kullanarak Application Insight telemetri verilerinin analizi</span><span class="sxs-lookup"><span data-stu-id="cb990-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="cb990-164">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="cb990-164">Create and run applications</span></span>
* [<span data-ttu-id="cb990-165">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb990-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="cb990-166">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="cb990-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="cb990-167">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="cb990-167">Tools and extensions</span></span>
* [<span data-ttu-id="cb990-168">Spark Scala uygulamaları oluşturmak ve göndermek amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisini kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="cb990-169">Spark uygulamalarında uzaktan hata ayıklamak amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="cb990-170">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="cb990-171">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="cb990-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="cb990-172">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="cb990-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="cb990-173">Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="cb990-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="cb990-174">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="cb990-174">Manage resources</span></span>
* [<span data-ttu-id="cb990-175">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="cb990-175">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="cb990-176">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="cb990-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
