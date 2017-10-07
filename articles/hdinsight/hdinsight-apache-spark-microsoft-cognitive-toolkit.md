---
title: "aaaMicrosoft Azure Hdınsight Spark ile kavrama Araç Seti için derin öğrenme | Microsoft Docs"
description: "Eğitilmiş bir Microsoft Bilişsel araç nasıl derin learning modeli Azure Hdınsight Spark kümesinde hello Spark Python API kullanarak uygulanan tooa dataset olabilir öğrenin."
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
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="9f291-103">Microsoft Azure Hdınsight Spark küme modeliyle öğrenme derin bir Bilişsel araç kullanma</span><span class="sxs-lookup"><span data-stu-id="9f291-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="9f291-104">Bu makaledeki adımları izleyerek hello.</span><span class="sxs-lookup"><span data-stu-id="9f291-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="9f291-105">Özel bir komut dosyası tooinstall Microsoft Bilişsel Araç Seti Azure Hdınsight Spark kümesi üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9f291-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="9f291-106">Bir Jupyter not defteri toohello Spark küme toosee nasıl karşıya tooapply bir eğitilen Microsoft Bilişsel Araç Seti modeli toofiles hello kullanarak bir Azure Blob Storage hesabında öğrenme derin [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="9f291-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f291-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9f291-107">Prerequisites</span></span>

* <span data-ttu-id="9f291-108">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="9f291-108">**An Azure subscription**.</span></span> <span data-ttu-id="9f291-109">Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f291-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="9f291-110">Bkz. [Ücretsiz Azure hesabınızı hemen oluşturun](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="9f291-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="9f291-111">**Azure Hdınsight Spark kümesi**.</span><span class="sxs-lookup"><span data-stu-id="9f291-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="9f291-112">Bu makalede, bir Spark 2.0 kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f291-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="9f291-113">Yönergeler için bkz: [Azure hdınsight'ta Apache Spark oluşturma küme](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9f291-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="9f291-114">Bu çözümün nasıl akıyor?</span><span class="sxs-lookup"><span data-stu-id="9f291-114">How does this solution flow?</span></span>

<span data-ttu-id="9f291-115">Bu çözüm, bu makalede ve bu öğreticinin bir parçası olarak karşıya Jupyter not defteri arasında bölünür.</span><span class="sxs-lookup"><span data-stu-id="9f291-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="9f291-116">Bu makalede, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="9f291-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="9f291-117">Betik eylemi bir Hdınsight Spark kümesinde tooinstall Microsoft Bilişsel Araç Seti ve Python paketlerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9f291-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="9f291-118">Merhaba çözüm toohello Hdınsight Spark kümesinde çalışan hello Jupyter not defteri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9f291-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="9f291-119">Merhaba bir hello Jupyter Not Defteri en aşağıdaki kalan adımları ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="9f291-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="9f291-120">Yük örnek görüntülere Spark Resiliant dağıtılmış Dataset ya da RDD</span><span class="sxs-lookup"><span data-stu-id="9f291-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="9f291-121">Modülleri yüklemek ve hazır tanımlayın</span><span class="sxs-lookup"><span data-stu-id="9f291-121">Load modules and define presets</span></span>
   - <span data-ttu-id="9f291-122">Merhaba dataset hello Spark kümesinde yerel olarak indir</span><span class="sxs-lookup"><span data-stu-id="9f291-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="9f291-123">Bir RDD Hello dataset Dönüştür</span><span class="sxs-lookup"><span data-stu-id="9f291-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="9f291-124">Bilişsel Araç Seti modeli kullanarak puan hello görüntüleri</span><span class="sxs-lookup"><span data-stu-id="9f291-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="9f291-125">Eğitilmiş hello Bilişsel Araç Seti modeli toohello Spark kümesi indirin</span><span class="sxs-lookup"><span data-stu-id="9f291-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="9f291-126">Alt düğümler tarafından kullanılan işlevler toobe tanımlayın</span><span class="sxs-lookup"><span data-stu-id="9f291-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="9f291-127">Çalışan düğümü puan hello görüntülerde</span><span class="sxs-lookup"><span data-stu-id="9f291-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="9f291-128">Model doğruluğundan değerlendir</span><span class="sxs-lookup"><span data-stu-id="9f291-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="9f291-129">Microsoft Bilişsel Araç Seti yükleyin</span><span class="sxs-lookup"><span data-stu-id="9f291-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="9f291-130">Betik eylemi kullanarak Spark kümesinde Microsoft Bilişsel Araç Seti yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f291-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="9f291-131">Betik eylemi özel komut dosyaları tooinstall bileşenler varsayılan olarak kullanılabilir değil hello kümede kullanır.</span><span class="sxs-lookup"><span data-stu-id="9f291-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="9f291-132">Hdınsight .NET SDK kullanarak ya da Azure PowerShell kullanarak hello Azure Portal, özel betikten hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f291-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="9f291-133">Merhaba betik tooinstall hello Araç Seti parçası olarak küme oluşturma veya hello küme hazır ve çalışır sonra aşağıdakilerden birini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f291-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="9f291-134">Bu makalede, Hello Küme oluşturulduktan sonra hello portal tooinstall hello araç seti, kullanırız.</span><span class="sxs-lookup"><span data-stu-id="9f291-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="9f291-135">Diğer yolları toorun hello özel komut dosyaları için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9f291-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="9f291-136">Hello Azure Portal kullanarak</span><span class="sxs-lookup"><span data-stu-id="9f291-136">Using hello Azure Portal</span></span>

<span data-ttu-id="9f291-137">Toouse hello Azure Portal toorun eylem nasıl komut dosyası ile ilgili yönergeler için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="9f291-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="9f291-138">Girişleri tooinstall Microsoft Bilişsel Araç Seti aşağıdaki hello sağladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9f291-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="9f291-139">Merhaba betik eylem adı için bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="9f291-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="9f291-140">İçin **betik URI Bash**, girin `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="9f291-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="9f291-141">Head ve çalışan düğümleri üzerinde yalnızca hello hello komut dosyasını çalıştırın ve tüm diğer onay kutularını temizleyin hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="9f291-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="9f291-142">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9f291-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="9f291-143">Merhaba Jupyter not defteri tooAzure Hdınsight Spark kümesi karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="9f291-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="9f291-144">toouse hello Microsoft Bilişsel Araç Seti hello Azure Hdınsight Spark kümesinde ile Merhaba Jupyter not defteri yüklemelisiniz **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure Hdınsight Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="9f291-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="9f291-145">Bu not defteri github'da kullanılabilir [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="9f291-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="9f291-146">Kopya hello GitHub deposunu [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="9f291-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="9f291-147">Yönergeler tooclone için bkz: [depo kopyalama](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="9f291-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="9f291-148">Zaten sağlanmış tıklatın hello Spark kümesi dikey Hello Azure Portalı ' açmak **küme Panosu**ve ardından **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="9f291-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="9f291-149">Toohello URL giderek hello Jupyter not defteri başlatabilirsiniz `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="9f291-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="9f291-150">Değiştir \<clustername > Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="9f291-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="9f291-151">Merhaba Jupyter not defteri tıklatın **karşıya** hello sağ üst köşesinde ve hello GitHub deposunu kopyaladığınız toohello konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="9f291-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="9f291-152">![Hdınsight Spark kümesinde Jupyter not defteri tooAzure karşıya](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "karşıya Jupyter not defteri tooAzure Hdınsight Spark kümesi")</span><span class="sxs-lookup"><span data-stu-id="9f291-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="9f291-153">Tıklatın **karşıya** yeniden.</span><span class="sxs-lookup"><span data-stu-id="9f291-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="9f291-154">Hello dizüstü karşıya yüklendikten sonra hello dizüstü hello adına tıklayın ve ardından nasıl tooload veri kümesi hello ve hello öğretici gerçekleştirmek hello Not kendisini hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="9f291-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="9f291-155">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9f291-155">See also</span></span>
* [<span data-ttu-id="9f291-156">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="9f291-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="9f291-157">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="9f291-157">Scenarios</span></span>
* [<span data-ttu-id="9f291-158">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="9f291-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9f291-159">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="9f291-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="9f291-160">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="9f291-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9f291-161">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="9f291-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9f291-162">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="9f291-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="9f291-163">HDInsight’ta Spark kullanarak Application Insight telemetri verilerinin analizi</span><span class="sxs-lookup"><span data-stu-id="9f291-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="9f291-164">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9f291-164">Create and run applications</span></span>
* [<span data-ttu-id="9f291-165">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f291-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9f291-166">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9f291-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9f291-167">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="9f291-167">Tools and extensions</span></span>
* [<span data-ttu-id="9f291-168">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="9f291-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9f291-169">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="9f291-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="9f291-170">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="9f291-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9f291-171">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="9f291-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9f291-172">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="9f291-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9f291-173">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="9f291-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="9f291-174">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="9f291-174">Manage resources</span></span>
* [<span data-ttu-id="9f291-175">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="9f291-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9f291-176">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="9f291-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
