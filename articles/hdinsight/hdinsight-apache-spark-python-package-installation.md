---
title: "aaaScript eylemi - Azure hdınsight'ta Jupyter ile yükleme Python paketlerini | Microsoft Docs"
description: "Nasıl toouse betik eylemi tooconfigure Jupyter not defterleri ile Hdınsight Spark kullanılabilir kümeleri toouse dış python paketlerini ilişkin adım adım yönergeler için."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="8c570-103">Hdınsight'ta Apache Spark kümeleri Jupyter not defterlerinde için betik eylemi tooinstall dış Python paketlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c570-104">Hücre Sihirli kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="8c570-105">Betik eylemi kullanarak</span><span class="sxs-lookup"><span data-stu-id="8c570-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="8c570-106">Nasıl toouse betik eylemleri tooconfigure Hdınsight (Linux) toouse dış, Apache Spark kümesinde topluluk-katkıda öğrenin **python** hello kümede olmayan paketler dahil Giden kutusu.</span><span class="sxs-lookup"><span data-stu-id="8c570-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8c570-107">Jupyter Not Defteri kullanarak da yapılandırabilirsiniz `%%configure` Sihirli toouse dış paketler.</span><span class="sxs-lookup"><span data-stu-id="8c570-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="8c570-108">Yönergeler için bkz: [hdınsight'ta Apache Spark kümeleri Jupyter not defterlerinde ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8c570-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="8c570-109">Merhaba arayabilirsiniz [paket dizini](https://pypi.python.org/pypi) hello tam kullanılabilir paketler listesi.</span><span class="sxs-lookup"><span data-stu-id="8c570-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="8c570-110">Ayrıca, diğer kaynaklardan kullanılabilir paketlerin listesini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c570-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="8c570-111">Örneğin, kullanılabilir hale paketlerini yükleyebilirsiniz [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) veya [conda oluşturmasına](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="8c570-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="8c570-112">Bu makalede, öğreneceksiniz nasıl tooinstall hello [TensorFlow](https://www.tensorflow.org/) kümenizde betik Actoin kullanarak paketini ve hello Jupyter not defteri kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c570-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c570-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8c570-113">Prerequisites</span></span>
<span data-ttu-id="8c570-114">Merhaba şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8c570-114">You must have hello following:</span></span>

* <span data-ttu-id="8c570-115">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8c570-115">An Azure subscription.</span></span> <span data-ttu-id="8c570-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8c570-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8c570-117">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="8c570-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8c570-118">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8c570-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c570-119">Hdınsight Linux üzerinde Spark kümesi zaten yoksa, küme oluşturma sırasında betik eylemleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c570-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="8c570-120">Merhaba belgeleri ziyaret [toouse özel eylemler nasıl komut dosyası](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="8c570-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="8c570-121">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="8c570-122">Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c570-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="8c570-123">Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="8c570-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="8c570-124">Merhaba Spark kümesi dikey penceresinden tıklatın **betik eylemleri** altında **kullanım**.</span><span class="sxs-lookup"><span data-stu-id="8c570-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="8c570-125">Merhaba baş düğümler ve hello çalışan düğümleri TensorFlow yükler hello özel eylemini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8c570-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="8c570-126">Merhaba bash komut dosyası, gelen başvurulabilir: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh ziyaret hello belgelerine [toouse özel eylemler nasıl komut dosyası](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="8c570-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c570-127">Merhaba küme yüklemelerde iki python vardır.</span><span class="sxs-lookup"><span data-stu-id="8c570-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="8c570-128">Spark hello Anaconda python yükleme konumunda bulunan kullanacağınız `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="8c570-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="8c570-129">Bu yükleme, özel eylemleri başvuru `/usr/bin/anaconda/bin/pip` ve `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="8c570-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="8c570-130">Bir PySpark Jupyter not defteri açın</span><span class="sxs-lookup"><span data-stu-id="8c570-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="8c570-131">![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Yeni bir Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="8c570-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="8c570-132">Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile.</span><span class="sxs-lookup"><span data-stu-id="8c570-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="8c570-133">Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8c570-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="8c570-134">![Merhaba dizüstü bilgisayar için bir ad](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "hello dizüstü bilgisayar için bir ad sağlayın")</span><span class="sxs-lookup"><span data-stu-id="8c570-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="8c570-135">Şimdi olacak `import tensorflow` ve Merhaba Dünya örneği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8c570-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="8c570-136">Kod toocopy:</span><span class="sxs-lookup"><span data-stu-id="8c570-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="8c570-137">Merhaba sonuç şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="8c570-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="8c570-138">![TensorFlow kod yürütmeyi](./media/hdinsight-apache-spark-python-package-installation/execution.png "yürütme TensorFlow kodu")</span><span class="sxs-lookup"><span data-stu-id="8c570-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="8c570-139"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8c570-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8c570-140">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="8c570-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8c570-141">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="8c570-141">Scenarios</span></span>
* [<span data-ttu-id="8c570-142">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="8c570-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8c570-143">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8c570-144">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8c570-145">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="8c570-146">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="8c570-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8c570-147">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8c570-147">Create and run applications</span></span>
* [<span data-ttu-id="8c570-148">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c570-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8c570-149">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8c570-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8c570-150">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="8c570-150">Tools and extensions</span></span>
* [<span data-ttu-id="8c570-151">Hdınsight'ta Apache Spark kümeleri Jupyter not defterlerinde ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="8c570-152">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="8c570-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8c570-153">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8c570-154">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="8c570-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8c570-155">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="8c570-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8c570-156">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="8c570-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8c570-157">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="8c570-157">Manage resources</span></span>
* [<span data-ttu-id="8c570-158">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8c570-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8c570-159">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="8c570-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
