---
title: "aaaData Bilim Scala ve Spark Azure üzerinde kullanarak | Microsoft Docs"
description: "Nasıl toouse Scala denetimli machine learning ile görevleri için Spark ölçeklenebilir Mllib'i ve Spark ML paketleri Azure Hdınsight Spark kümesinde hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="4ea75-103">Azure üzerinde Scala ve Spark kullanan Veri Bilimi</span><span class="sxs-lookup"><span data-stu-id="4ea75-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="4ea75-104">Bu makale bir Azure Hdınsight Spark kümesinde nasıl toouse Scala denetimli makine öğrenimi görevlerini hello Spark ölçeklenebilir Mllib'i ve Spark ML için paketler gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="4ea75-105">Merhaba oluşturduğunu hello görevlerinde anlatılmaktadır [veri bilimi işlem](http://aka.ms/datascienceprocess): veri alımı ve keşfi, görselleştirme, özellik Mühendisliği, model ve model tüketim.</span><span class="sxs-lookup"><span data-stu-id="4ea75-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="4ea75-106">hello makale Hello modellerinde Lojistik ve doğrusal regresyon, rastgele ormanları ve gradyan boosted ağaçları (GBTs) dahil, ayrıca tootwo ortak makine öğrenimi görevlerini denetimli:</span><span class="sxs-lookup"><span data-stu-id="4ea75-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="4ea75-107">Regresyon sorunu: Tahmin ücreti seyahat için hello ipucu tutar ($)</span><span class="sxs-lookup"><span data-stu-id="4ea75-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="4ea75-108">İkili sınıflandırma: tahmin ipucu veya ücreti seyahat için ipucu yok (1/0)</span><span class="sxs-lookup"><span data-stu-id="4ea75-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="4ea75-109">İşlem modelleme hello eğitim ve sınama veri kümesi ve ilgili doğruluğu ölçümleri değerlendirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="4ea75-110">Bu makalede, toostore bunlar nasıl modelleri de öğrenebilirsiniz Azure Blob Depolama ve nasıl tooscore ve Tahmine dayalı kendi performansını değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="4ea75-111">Bu makale çapraz doğrulama ve parametre hyper Süpürme kullanarak toooptimize nasıl modeller, konuları daha gelişmiş hello da kapsar.</span><span class="sxs-lookup"><span data-stu-id="4ea75-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="4ea75-112">kullanılan hello verileri hello 2013 NYC ücreti seyahat ve ücreti veri kümesinin Github'da bulunan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="4ea75-113">[Scala](http://www.scala-lang.org/), nesne yönelimli ve işlevsel dil kavramları hello Java sanal makineye bağlı bir dil tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="4ea75-114">Bu, hello bulutta işleme uygun toodistributed ve Azure Spark kümeleri üzerinde çalışan ölçeklenebilir bir dildir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="4ea75-115">[Spark](http://spark.apache.org/) bellek içi destekleyen bir açık kaynak paralel işleme altyapısıdır işliyor tooboost hello büyük veri analizi uygulamalarının performansını.</span><span class="sxs-lookup"><span data-stu-id="4ea75-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="4ea75-116">Merhaba Spark işleme altyapısı hızı, kullanımı kolay, gelişmiş analizler için yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="4ea75-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="4ea75-117">Spark'ın bellek içi dağıtılmış hesaplama özellikleri machine learning ve grafik hesaplamalarında yinelemeli algoritmalar için iyi bir seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="4ea75-118">Merhaba [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) paket yardımcı olabilecek çerçeveleri oluşturmak ve ardışık düzen öğrenme pratik makine ayarlamak veri üstünde yerleşik yüksek düzey API'leri Tekdüzen kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ea75-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="4ea75-119">[Mllib'i](http://spark.apache.org/mllib/) modelleme yetenekleri getirir Spark'ın ölçeklenebilir machine learning kitaplığı toothis dağıtılmış ortamı.</span><span class="sxs-lookup"><span data-stu-id="4ea75-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="4ea75-120">[Hdınsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure barındırılan açık kaynak Spark, bir tekliftir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="4ea75-121">Merhaba Spark kümesinde Jupyter Scala dizüstü bilgisayarlar için destek de içerir ve çalışma Spark SQL etkileşimli sorguları tootransform filtre uygulayabilir ve Azure Blob depolamada depolanan verileri görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="4ea75-122">Merhaba çözümleri sağlayan ve hello ilgili çizimleri toovisualize hello verileri göster hello Scala kod parçacıkları bu makalede hello Spark kümeleri üzerinde yüklü Jupyter not defterleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="4ea75-123">Aşağıdaki konulardaki Hello modelleme adımları nasıl tootrain, değerlendirmek, kaydetme ve kullanmayı modelinin yazın ve her gösteren kod sahip.</span><span class="sxs-lookup"><span data-stu-id="4ea75-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="4ea75-124">Merhaba kurulum adımlarını ve bu makaledeki kod için Azure Hdınsight 3.4 Spark 1.6 markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="4ea75-125">Ancak, bu makaledeki ve hello kodu hello [Scala Jupyter not defteri](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) geneldir ve tüm Spark kümesi üzerinde çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="4ea75-126">Küme kurulumu hello ve bir yönetim adımı Hdınsight Spark kullanmıyorsanız ne bu makalede gösterilenden biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="4ea75-127">Nasıl bir uçtan uca veri bilimi işlemi toouse Scala yerine Python toocomplete görevleri gösterir bir konuya bakın [veri bilimi Azure Hdınsight'ta Spark kullanmanın](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ea75-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4ea75-128">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4ea75-128">Prerequisites</span></span>
* <span data-ttu-id="4ea75-129">Bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-129">You must have an Azure subscription.</span></span> <span data-ttu-id="4ea75-130">Zaten bir yoksa [Azure ücretsiz deneme sürümünü edinin](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4ea75-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4ea75-131">Yordamları izleyerek bir Azure Hdınsight 3.4 Spark 1.6 küme toocomplete hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="4ea75-132">toocreate bir küme bkz hello yönergeleri [Başlarken: Azure hdınsight'ta Apache Spark oluşturmak](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4ea75-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="4ea75-133">Merhaba üzerinde hello küme türü ve sürümü ayarlama **küme türü seçin** menüsü.</span><span class="sxs-lookup"><span data-stu-id="4ea75-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![Hdınsight küme türü yapılandırma](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="4ea75-135">Merhaba NYC ücreti seyahat veri ve nasıl tooexecute kod hello Spark kümesinde Jupyter not defteri gelen yönergeleri açıklaması için hello ilgili bölümlere bakın [genel bakış, verileri Azure Hdınsight'ta Spark kullanmanın Bilim](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ea75-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="4ea75-136">Merhaba Spark kümesinde Jupyter not defteri gelen Scala kodu yürütme</span><span class="sxs-lookup"><span data-stu-id="4ea75-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="4ea75-137">Jupyter not defteri hello Azure Portalı'ndan başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="4ea75-138">Panonuz Hello Spark kümesinde bulun ve sonra tooenter hello Yönetim sayfasında kümeniz için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="4ea75-139">Bundan sonra öğesini **küme panolarında**ve ardından **Jupyter not defteri** tooopen hello not defteri hello Spark kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="4ea75-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![Küme panosu ve Jupyter Not Defterleri](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="4ea75-141">Jupyter not defterleri https:// sırasında da erişebilirsiniz&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="4ea75-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="4ea75-142">Değiştir *clustername* kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="4ea75-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="4ea75-143">Yönetici hesabı tooaccess hello Jupyter not defterlerinizi için başlangıç parolası gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Merhaba küme adını kullanarak tooJupyter not defterlerini gidin](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="4ea75-145">Seçin **Scala** toosee paketlenmiş not defterlerini birkaçı bu kullanım hello PySpark API sahip bir dizini.</span><span class="sxs-lookup"><span data-stu-id="4ea75-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="4ea75-146">Merhaba kod örnekleri üzerinde Spark konular bu paketi kullanılabilir içeren Scala.ipynb Not Defteri kullanarak araştırması modelleme ve puanlama hello [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="4ea75-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="4ea75-147">Spark kümesinde hello dizüstü GitHub toohello Jupyter not defteri sunucu doğrudan karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="4ea75-148">Merhaba, Jupyter giriş sayfasında, tıklatın **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4ea75-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="4ea75-149">Merhaba dosya Gezgini'nde, hello GitHub (Ham içerik) hello Scala dizüstü URL'sini yapıştırın ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="4ea75-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="4ea75-150">Merhaba Scala dizüstü URL aşağıdaki hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="4ea75-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="4ea75-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="4ea75-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="4ea75-152">Kurulumu: Hazır Spark ve Hive bağlamları, Spark sihirler ve Spark kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="4ea75-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="4ea75-153">Spark ve Hive bağlamları hazır</span><span class="sxs-lookup"><span data-stu-id="4ea75-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="4ea75-154">Jupyter not defterleri ile sağlanan hello Spark tekrar hazır bağlamları vardır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="4ea75-155">Geliştirdiğiniz Merhaba uygulaması ile çalışmaya başlamadan önce tooexplicitly kümesi hello Spark veya Hive bağlamları gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4ea75-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="4ea75-156">Merhaba hazır bağlamları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4ea75-156">hello preset contexts are:</span></span>

* <span data-ttu-id="4ea75-157">`sc`SparkContext için</span><span class="sxs-lookup"><span data-stu-id="4ea75-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="4ea75-158">`sqlContext`HiveContext için</span><span class="sxs-lookup"><span data-stu-id="4ea75-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="4ea75-159">Spark sihirler</span><span class="sxs-lookup"><span data-stu-id="4ea75-159">Spark magics</span></span>
<span data-ttu-id="4ea75-160">Merhaba Spark çekirdek bazı önceden tanımlanmış "sihirleri" ile çağırabilir özel komutlar olduğu sağlar `%%`.</span><span class="sxs-lookup"><span data-stu-id="4ea75-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="4ea75-161">Bu komutların iki kod örnekleri aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="4ea75-162">`%%local`sonraki satırların Hello kodda yerel olarak yürütülecek belirtir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="4ea75-163">Merhaba kodu geçerli Scala kodu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="4ea75-164">`%%sql -o <variable name>`bir Hive sorgusu yürütür `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="4ea75-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="4ea75-165">Merhaba, `-o` parametresi geçirilir, hello hello sorgunun sonucu hello kalıcı `%%local` Scala bağlamı Spark veri çerçeve olarak.</span><span class="sxs-lookup"><span data-stu-id="4ea75-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="4ea75-166">İle arama, hello tekrar Jupyter not defterlerini ve bunların önceden tanımlanmış hakkında daha fazla bilgi "magics için" `%%` (örneğin, `%%local`), bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Hdınsight Spark Linux kümeleri Hdınsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="4ea75-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="4ea75-167">Kitaplıkları içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="4ea75-167">Import libraries</span></span>
<span data-ttu-id="4ea75-168">Merhaba Spark, Mllib'i ve koddan hello kullanarak gerekir diğer kitaplıkları içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a><span data-ttu-id="4ea75-169">Veri alımı</span><span class="sxs-lookup"><span data-stu-id="4ea75-169">Data ingestion</span></span>
<span data-ttu-id="4ea75-170">Merhaba ilk hello veri bilimi işlem tooanalyze istediğiniz tooingest hello veri adımdır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="4ea75-171">Veri keşfi ve modelleme ortamınıza bulunduğu hello veri dış kaynaklara veya sistemlerinden getirin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="4ea75-172">Bu makalede, alma hello veri bir birleştirilmiş % 0,1 (.tsv dosyası olarak depolanır) hello ücreti seyahat ve ücreti dosyası örneğidir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="4ea75-173">Merhaba veri keşfi ve modelleme Spark ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="4ea75-174">Bu bölümde, görev dizisini aşağıdaki hello kod toocomplete hello içerir:</span><span class="sxs-lookup"><span data-stu-id="4ea75-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="4ea75-175">Depolama veri ve model için dizin yolu olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="4ea75-176">Merhaba giriş veri kümesindeki (bir .tsv dosyası olarak depolanır) okuyun.</span><span class="sxs-lookup"><span data-stu-id="4ea75-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="4ea75-177">Merhaba verileri ve temiz hello verileri için bir şema tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="4ea75-178">Temizlenen veri çerçevesi oluşturun ve bellekte önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="4ea75-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="4ea75-179">Merhaba veri SQLContext geçici tablo olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="4ea75-180">Merhaba Tablo Sorgu ve veri çerçeveye hello sonuçları alın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="4ea75-181">Dizin yolları depolama konumları için Azure Blob depolama alanına ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4ea75-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="4ea75-182">Spark okuma ve tooAzure Blob Depolama yazma.</span><span class="sxs-lookup"><span data-stu-id="4ea75-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="4ea75-183">Mevcut verilerinizi Spark tooprocess kullanın ve ardından hello sonuçları Blob storage'da depolamak.</span><span class="sxs-lookup"><span data-stu-id="4ea75-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="4ea75-184">toosave modelleri veya Blob storage'da dosyaları, gereksinim duyduğunuz tooproperly hello yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="4ea75-185">Başvuru hello varsayılan kapsayıcı bağlı toohello Spark kümesi ile başlayan bir yolu kullanarak `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="4ea75-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="4ea75-186">Diğer konumları kullanarak başvuru `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="4ea75-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="4ea75-187">Merhaba aşağıdaki kod örneği hello giriş verisi toobe okuyun ve ekli toohello Spark küme hello yolu tooBlob depolama hello modeli kaydedileceği hello konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="4ea75-188">Veri alma, bir RDD oluşturun ve toohello şemasına göre bir veri çerçevesi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="4ea75-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="4ea75-189">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-189">**Output:**</span></span>

<span data-ttu-id="4ea75-190">Zaman toorun hello hücre: 8 saniye.</span><span class="sxs-lookup"><span data-stu-id="4ea75-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="4ea75-191">Merhaba Tablo Sorgu ve veri çerçevesinde sonuçları Al</span><span class="sxs-lookup"><span data-stu-id="4ea75-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="4ea75-192">Ardından, ücreti, yolcu ve ipucu veri için sorgu hello tablosu; bozuk ve harici verilerini filtre; ve birkaç satır yazdırın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="4ea75-193">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-193">**Output:**</span></span>

| <span data-ttu-id="4ea75-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="4ea75-194">fare_amount</span></span> | <span data-ttu-id="4ea75-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="4ea75-195">passenger_count</span></span> | <span data-ttu-id="4ea75-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="4ea75-196">tip_amount</span></span> | <span data-ttu-id="4ea75-197">Eğimli</span><span class="sxs-lookup"><span data-stu-id="4ea75-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="4ea75-198">13.5</span><span class="sxs-lookup"><span data-stu-id="4ea75-198">13.5</span></span> |<span data-ttu-id="4ea75-199">1.0</span><span class="sxs-lookup"><span data-stu-id="4ea75-199">1.0</span></span> |<span data-ttu-id="4ea75-200">2.9</span><span class="sxs-lookup"><span data-stu-id="4ea75-200">2.9</span></span> |<span data-ttu-id="4ea75-201">1.0</span><span class="sxs-lookup"><span data-stu-id="4ea75-201">1.0</span></span> |
|        <span data-ttu-id="4ea75-202">16.0</span><span class="sxs-lookup"><span data-stu-id="4ea75-202">16.0</span></span> |<span data-ttu-id="4ea75-203">2.0</span><span class="sxs-lookup"><span data-stu-id="4ea75-203">2.0</span></span> |<span data-ttu-id="4ea75-204">3.4</span><span class="sxs-lookup"><span data-stu-id="4ea75-204">3.4</span></span> |<span data-ttu-id="4ea75-205">1.0</span><span class="sxs-lookup"><span data-stu-id="4ea75-205">1.0</span></span> |
|        <span data-ttu-id="4ea75-206">10.5</span><span class="sxs-lookup"><span data-stu-id="4ea75-206">10.5</span></span> |<span data-ttu-id="4ea75-207">2.0</span><span class="sxs-lookup"><span data-stu-id="4ea75-207">2.0</span></span> |<span data-ttu-id="4ea75-208">1.0</span><span class="sxs-lookup"><span data-stu-id="4ea75-208">1.0</span></span> |<span data-ttu-id="4ea75-209">1.0</span><span class="sxs-lookup"><span data-stu-id="4ea75-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="4ea75-210">Veri keşfi ve görselleştirme</span><span class="sxs-lookup"><span data-stu-id="4ea75-210">Data exploration and visualization</span></span>
<span data-ttu-id="4ea75-211">Spark hello verileri aldıktan sonra hello sonraki hello veri bilimi işlem toogain hello veri keşfi ve görselleştirme aracılığıyla daha derin bir anlayış adımdır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="4ea75-212">Bu bölümde, SQL sorguları kullanarak hello ücreti verileri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="4ea75-213">Ardından, bir veri çerçeve tooplot içine hello sonuçlarını içeri aktar hedef değişkenleri ve görsel İnceleme için olası özellikleri Jupyter hello otomatik görselleştirme özelliğini kullanarak hello.</span><span class="sxs-lookup"><span data-stu-id="4ea75-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="4ea75-214">Yerel ve SQL Sihirli tooplot veri kullanın</span><span class="sxs-lookup"><span data-stu-id="4ea75-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="4ea75-215">Varsayılan olarak, Jupyter not defteri çalıştırmak herhangi kod parçacığını hello çıktısını hello çalışan düğümlerine kalıcı hello oturumunun hello bağlam içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="4ea75-216">Tüm (Merhaba baş düğüm olan) yerel olarak hello Jupyter sunucu düğümünde, hesaplama için gereksinim duyduğunuz verileri Merhaba, hello kullanabilirsiniz ve her hesaplama için seyahat toohello çalışan düğümleri toosave isterseniz `%%local` Sihirli toorun hello kodu kod parçacığında hello Jupyter sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="4ea75-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="4ea75-217">**SQL Sihirli** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="4ea75-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="4ea75-218">Merhaba Hdınsight Spark çekirdek SQLContext kolay satır içi HiveQL sorguları destekler.</span><span class="sxs-lookup"><span data-stu-id="4ea75-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="4ea75-219">Merhaba (`-o VARIABLE_NAME`) bağımsız değişkeni devam ederse hello SQL sorgusu hello çıktısını hello Jupyter sunucuda Pandas veri çerçeve olarak.</span><span class="sxs-lookup"><span data-stu-id="4ea75-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="4ea75-220">Başka bir deyişle, hello yerel modda kullanılabilir olması.</span><span class="sxs-lookup"><span data-stu-id="4ea75-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="4ea75-221">`%%local`**Sihirli**.</span><span class="sxs-lookup"><span data-stu-id="4ea75-221">`%%local` **magic**.</span></span> <span data-ttu-id="4ea75-222">Merhaba `%%local` Sihirli çalıştıran hello kod yerel olarak hello Hdınsight kümesi baş düğüm hello hello Jupyter sunucu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="4ea75-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="4ea75-223">Genellikle, kullandığınız `%%local` hello birlikte Sihirli `%%sql` hello ile Sihirli `-o` parametresi.</span><span class="sxs-lookup"><span data-stu-id="4ea75-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="4ea75-224">Merhaba `-o` parametresi yerel olarak hello SQL sorgusu hello çıktısını kalıcı ve ardından `%%local` Sihirli hello sonraki kod parçacığını toorun yerel olarak yerel olarak kalıcı hello çıktı hello SQL sorgularının karşı kümesini tetiklemek.</span><span class="sxs-lookup"><span data-stu-id="4ea75-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="4ea75-225">SQL kullanarak Hello veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="4ea75-225">Query hello data by using SQL</span></span>
<span data-ttu-id="4ea75-226">Bu sorgu hello ücreti dönüşleri ücreti tutarı, yolcu sayısı ve ipucu miktarını alır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="4ea75-227">Koddan hello hello `%%local` Sihirli sqlResults bir yerel veri çerçevesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4ea75-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="4ea75-228">Matplotlib kullanarak sqlResults tooplot kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="4ea75-229">Yerel Sihirli birden çok kez bu makalede kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="4ea75-230">Veri kümenizi büyük olursa, lütfen toocreate yerel belleğe sığması veri çerçevesi örnek.</span><span class="sxs-lookup"><span data-stu-id="4ea75-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="4ea75-231">Çizim hello veri</span><span class="sxs-lookup"><span data-stu-id="4ea75-231">Plot hello data</span></span>
<span data-ttu-id="4ea75-232">Yerel bağlamı Pandas veri çerçeve olarak hello veri çerçevesi olduktan sonra Python kodu kullanarak çizebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="4ea75-233">Merhaba kod çalıştırdıktan sonra hello Spark çekirdek (HiveQL) SQL sorguları hello çıktısını otomatik olarak visualizes.</span><span class="sxs-lookup"><span data-stu-id="4ea75-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="4ea75-234">Görselleştirmeleri çeşitli türleri arasında seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4ea75-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="4ea75-235">Tablo</span><span class="sxs-lookup"><span data-stu-id="4ea75-235">Table</span></span>
* <span data-ttu-id="4ea75-236">Pasta</span><span class="sxs-lookup"><span data-stu-id="4ea75-236">Pie</span></span>
* <span data-ttu-id="4ea75-237">Çizgi</span><span class="sxs-lookup"><span data-stu-id="4ea75-237">Line</span></span>
* <span data-ttu-id="4ea75-238">Alan</span><span class="sxs-lookup"><span data-stu-id="4ea75-238">Area</span></span>
* <span data-ttu-id="4ea75-239">Çubuğu</span><span class="sxs-lookup"><span data-stu-id="4ea75-239">Bar</span></span>

<span data-ttu-id="4ea75-240">Merhaba kod tooplot hello verileri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4ea75-240">Here's hello code tooplot hello data:</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


<span data-ttu-id="4ea75-241">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-241">**Output:**</span></span>

![İpucu tutar histogram](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Yolcu sayısına göre ipucu tutar](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![İpucu tutar ücreti miktar](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="4ea75-245">Özellikler oluşturmak ve özellikleri dönüştürme ve veri işlevleri modelleme içine girişi için hazırla</span><span class="sxs-lookup"><span data-stu-id="4ea75-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="4ea75-246">Spark ML ve Mllib'i ağaç tabanlı modelleme işlevleri için tooprepare hedef ve özellik binning, dizin oluşturma, bir seyrek kodlama ve vectorization gibi teknikler çeşitli kullanarak vardır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="4ea75-247">Bu bölümde hello yordamları toofollow şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4ea75-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="4ea75-248">Yeni bir özellik tarafından oluşturma **binning** trafiği saate demet saat.</span><span class="sxs-lookup"><span data-stu-id="4ea75-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="4ea75-249">Uygulama **dizin oluşturma ve bir hot kodlama** toocategorical özellikleri.</span><span class="sxs-lookup"><span data-stu-id="4ea75-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="4ea75-250">**Örnek ve bölünmüş hello veri kümesi** eğitim ve test kesirler içine.</span><span class="sxs-lookup"><span data-stu-id="4ea75-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="4ea75-251">**Eğitim değişken ve Özellikler belirtmek**, eğitim kodlanmış dizinlenmiş veya bir dinamik sonra oluşturmak ve esnek giriş etiketli noktası sınama Dağıtılmış veri kümeleri (RDDs) veya veri çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="4ea75-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="4ea75-252">Otomatik olarak **kategorilere ayırmak ve özellikleri ve hedefleri vectorize** toouse makine öğrenimi modellerini için girdi olarak.</span><span class="sxs-lookup"><span data-stu-id="4ea75-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="4ea75-253">Yeni bir özellik tarafından binning saatleri trafiği zaman demet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4ea75-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="4ea75-254">Bu kodu nasıl toocreate saatleri trafiği zamanına binning tarafından yeni bir özellik aralıkları ve nasıl toocache hello bellek ortaya çıkan veri çerçevede gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="4ea75-255">RDDs ve veri çerçevelerini art arda kullanıldığı önbelleğe alma tooimproved yürütme sürelerinin yol açar.</span><span class="sxs-lookup"><span data-stu-id="4ea75-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="4ea75-256">Buna göre aşağıdaki yordamlarını hello çeşitli aşamalarında RDDs ve veri çerçevelerini önbelleğe alacağız.</span><span class="sxs-lookup"><span data-stu-id="4ea75-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="4ea75-257">Dizin oluşturma ve bir hot kategorik özelliklerini kodlama</span><span class="sxs-lookup"><span data-stu-id="4ea75-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="4ea75-258">Modelleme hello ve Mllib'i işlevlerini kategorik giriş verisi toobe özelliklerle dizine veya önceki toouse kodlanmış gerektiren tahmin etmek.</span><span class="sxs-lookup"><span data-stu-id="4ea75-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="4ea75-259">Bu bölümde, nasıl gösterilir tooindex veya İşlevler modelleme hello giriş için kategorik özellikleri kodlayın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="4ea75-260">Merhaba modeline bağlı olarak, farklı şekillerde Modellerinizi kodlamak veya tooindex gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="4ea75-261">Örneğin, bir seyrek kodlama Lojistik ve doğrusal regresyon modeli gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="4ea75-262">Örneğin, üç kategoride özelliğiyle üç özellik sütunlara genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="4ea75-263">Her sütun, 0 veya 1 bir gözlem hello kategorisine bağlı olarak içerecektir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="4ea75-264">Mllib'i sağlar hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) bir hot kodlama için işlevi.</span><span class="sxs-lookup"><span data-stu-id="4ea75-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="4ea75-265">Bu Kodlayıcı sütununun etiket dizinlerini tooa ikili vektörlerinin en çok bir değerle tek bir-bir sütun eşler.</span><span class="sxs-lookup"><span data-stu-id="4ea75-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="4ea75-266">Bu kodlama ile Lojistik regresyon gibi sayısal değerli özellikleri beklediğiniz algoritmaları uygulanan toocategorical özellikleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="4ea75-267">Burada karakter dizelerdir yalnızca dört değişkenleri tooshow örnekler dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="4ea75-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="4ea75-268">Kategorik değişkenleri olarak sayısal değerleri tarafından temsil edilen diğer gibi değişkenleri hafta içi günü, ayrıca dizin oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="4ea75-269">Dizin oluşturma için kullanmak `StringIndexer()`ve bir hot kodlaması için `OneHotEncoder()` Mllib'i işlevlerden.</span><span class="sxs-lookup"><span data-stu-id="4ea75-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="4ea75-270">Kategorik özellikleri kodlanacağını ve kod tooindex hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4ea75-270">Here is hello code tooindex and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="4ea75-271">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-271">**Output:**</span></span>

<span data-ttu-id="4ea75-272">Zaman toorun hello hücre: 4 saniye.</span><span class="sxs-lookup"><span data-stu-id="4ea75-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="4ea75-273">Örnek ve bölünmüş veri kümesi eğitim ve test kesirler hello</span><span class="sxs-lookup"><span data-stu-id="4ea75-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="4ea75-274">Bu kod bir rastgele örnekleme hello verilerin (Bu örnekte, %25) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4ea75-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="4ea75-275">Örnekleme bu örneğin hello veri kümesinin toohello boyutu nedeniyle gerekli olmamasına karşın, hello makale, böylece bildiğiniz nasıl, örnek oluşturabilirsiniz gösterir nasıl toouse gerektiğinde kendi sorunları için.</span><span class="sxs-lookup"><span data-stu-id="4ea75-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="4ea75-276">Örnekleri büyük olduğunda modelleri eğitme sırada bu önemli zaman kazanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="4ea75-277">Ardından, bölme hello örnek eğitim bölümü (Bu örnekte, %75) ve bir test olarak sınıflandırma ve regresyon modelleme (Bu örnekte, %25) toouse parçası.</span><span class="sxs-lookup"><span data-stu-id="4ea75-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="4ea75-278">Eğitim sırasında kullanılan tooselect çapraz doğrulama Katlama olan bir (0 ve 1 arasında) rastgele bir sayıyı tooeach satır ("rand" sütununda) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="4ea75-279">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-279">**Output:**</span></span>

<span data-ttu-id="4ea75-280">Zaman toorun hello hücre: 2 saniye.</span><span class="sxs-lookup"><span data-stu-id="4ea75-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="4ea75-281">Eğitim değişken ve özellikleri belirtin ve sonra eğitim ve giriş noktası RDDs ya da veri çerçevelerini etiketli test kodlanmış dizinli veya bir hot oluşturun</span><span class="sxs-lookup"><span data-stu-id="4ea75-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="4ea75-282">Bu bölümde nasıl tooindex kategorik metin verileri olarak etiketli bir veri türü gelin ve tootrain ve test Mllib'i Lojistik regresyon ve diğer sınıflandırma modelleri kullanabilmeniz için kodlama gösterir kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="4ea75-283">Etiketli noktası, girdi verisi olarak machine learning algoritmaları Mllib'i çoğu tarafından gerektiği şekilde biçimlendirilmiş RDDs nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="4ea75-284">A [noktası etiketli](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) yerel bir vektör, yoğun veya seyrek, etiket/yanıt ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="4ea75-285">Bu kodda hello hedef (bağımlı) değişkeni ve hello özellikleri toouse tootrain modelleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="4ea75-286">Sonra eğitim ve giriş noktası RDDs ya da veri çerçevelerini etiketli test kodlanmış dizinlenmiş veya bir hot oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="4ea75-287">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-287">**Output:**</span></span>

<span data-ttu-id="4ea75-288">Zaman toorun hello hücre: 4 saniye.</span><span class="sxs-lookup"><span data-stu-id="4ea75-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="4ea75-289">Otomatik olarak kategorilere ayırmak ve makine öğrenimi modellerini için girdi olarak özellikleri ve hedefleri toouse vectorize</span><span class="sxs-lookup"><span data-stu-id="4ea75-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="4ea75-290">Hedef ve özellik Spark ML toocategorize hello toouse ağaç tabanlı modelleme işlevlerde kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="4ea75-291">Merhaba kod iki görevleri tamamlar:</span><span class="sxs-lookup"><span data-stu-id="4ea75-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="4ea75-292">Sınıflandırma için ikili hedef 0 veya 1 tooeach veri noktası 0 ile 1 arasında bir değer 0,5 eşik değerini kullanarak atayarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4ea75-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="4ea75-293">Otomatik olarak özellikleri kategorilere ayırır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-293">Automatically categorizes features.</span></span> <span data-ttu-id="4ea75-294">Bu özellik, herhangi bir özellik için farklı sayısal değerleri Hello sayısı 32'den az ise, kategorilere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="4ea75-295">Burada, bu iki görevler için hello kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-295">Here's hello code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="4ea75-296">İkili sınıflandırma modeli: bir ipucu Ücretli olup olmadığını tahmin etme</span><span class="sxs-lookup"><span data-stu-id="4ea75-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="4ea75-297">Bu bölümde, bir ipucu Ücretli desteklemediğini ikili sınıflandırma modelleri toopredict üç tür oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4ea75-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="4ea75-298">A **Lojistik regresyon modeli** hello Spark ML kullanarak `LogisticRegression()` işlevi</span><span class="sxs-lookup"><span data-stu-id="4ea75-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="4ea75-299">A **rastgele orman sınıflandırma modeli** hello Spark ML kullanarak `RandomForestClassifier()` işlevi</span><span class="sxs-lookup"><span data-stu-id="4ea75-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="4ea75-300">A **gradyan artırma ağacı sınıflandırma modeli** hello Mllib'i kullanarak `GradientBoostedTrees()` işlevi</span><span class="sxs-lookup"><span data-stu-id="4ea75-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="4ea75-301">Lojistik regresyon modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ea75-301">Create a logistic regression model</span></span>
<span data-ttu-id="4ea75-302">Ardından, hello Spark ML kullanarak Lojistik regresyon modeli oluşturma `LogisticRegression()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="4ea75-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="4ea75-303">Bir dizi adımı kodda derleme hello modeli oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4ea75-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="4ea75-304">**Tren hello modeli** bir parametre kümesi ile verileri.</span><span class="sxs-lookup"><span data-stu-id="4ea75-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="4ea75-305">**Merhaba modelini değerlendir** ölçümlerle sınama veri kümesi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="4ea75-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="4ea75-306">**Merhaba modeli kaydedin** gelecekteki tüketimi için Blob Depolama birimindeki.</span><span class="sxs-lookup"><span data-stu-id="4ea75-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="4ea75-307">**Puan hello modeli** karşı test verileri.</span><span class="sxs-lookup"><span data-stu-id="4ea75-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="4ea75-308">**Merhaba sonuçları çizim** özelliği (ROC) Eğriler işletim alıcı ile.</span><span class="sxs-lookup"><span data-stu-id="4ea75-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="4ea75-309">Bu yordamları hello kodunu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4ea75-309">Here's hello code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="4ea75-310">Yüklemek için Puanlama ve hello sonuçları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-310">Load, score, and save hello results.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="4ea75-311">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-311">**Output:**</span></span>

<span data-ttu-id="4ea75-312">Test verileri ROC 0.9827381497557599 =</span><span class="sxs-lookup"><span data-stu-id="4ea75-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="4ea75-313">Python yerel Pandas veri çerçeveleri tooplot hello ROC eğrisi üzerinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="4ea75-314">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-314">**Output:**</span></span>

![İpucu veya hiçbir ipucu ROC eğrisi](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="4ea75-316">Rastgele orman sınıflandırma modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ea75-316">Create a random forest classification model</span></span>
<span data-ttu-id="4ea75-317">Ardından, hello Spark ML kullanarak bir rastgele orman sınıflandırma modeli oluşturma `RandomForestClassifier()` işlev ve test verileri hello modeli değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="4ea75-318">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-318">**Output:**</span></span>

<span data-ttu-id="4ea75-319">Test verileri ROC 0.9847103571552683 =</span><span class="sxs-lookup"><span data-stu-id="4ea75-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="4ea75-320">GBT sınıflandırma modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ea75-320">Create a GBT classification model</span></span>
<span data-ttu-id="4ea75-321">Ardından, Mllib'i'nın kullanarak GBT sınıflandırma modeli oluşturma `GradientBoostedTrees()` işlev ve test verileri hello modeli değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="4ea75-322">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-322">**Output:**</span></span>

<span data-ttu-id="4ea75-323">ROC eğrisi alanında: 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="4ea75-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="4ea75-324">Regresyon modeli: ipucu miktarı tahmin etmek</span><span class="sxs-lookup"><span data-stu-id="4ea75-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="4ea75-325">Bu bölümde, iki tür regresyon modeli toopredict hello ipucu tutar oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4ea75-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="4ea75-326">A **regularized doğrusal regresyon modeli** hello Spark ML kullanarak `LinearRegression()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="4ea75-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="4ea75-327">Hello modeli kaydedin ve test verileri hello modelini değerlendir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="4ea75-328">A **gradyan artırmanın ağacı regresyon modeli** hello Spark ML kullanarak `GBTRegressor()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="4ea75-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="4ea75-329">Regularized doğrusal regresyon modelini oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ea75-329">Create a regularized linear regression model</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="4ea75-330">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-330">**Output:**</span></span>

<span data-ttu-id="4ea75-331">Zaman toorun hello hücre: 13 saniye.</span><span class="sxs-lookup"><span data-stu-id="4ea75-331">Time toorun hello cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="4ea75-332">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-332">**Output:**</span></span>

<span data-ttu-id="4ea75-333">R-sqr test verileri 0.5960320470835743 =</span><span class="sxs-lookup"><span data-stu-id="4ea75-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="4ea75-334">Ardından, sorgu hello test veri çerçevesi ve kullanım AutoVizWidget ve matplotlib toovisualize bunu sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="4ea75-335">Merhaba kod yerel veri çerçeve hello sorgu çıktısı oluşturur ve hello veri çizer.</span><span class="sxs-lookup"><span data-stu-id="4ea75-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="4ea75-336">Merhaba `%%local` Sihirli oluşturur yerel veri çerçeve `sqlResults`, hangi tooplot matplotlib ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="4ea75-337">Bu Spark Sihirli birden çok kez bu makalede kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4ea75-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="4ea75-338">Merhaba miktarda veri büyükse, toocreate yerel belleğe sığması veri çerçevesi örnek.</span><span class="sxs-lookup"><span data-stu-id="4ea75-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="4ea75-339">Çizimler, Python matplotlib kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4ea75-339">Create plots by using Python matplotlib.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="4ea75-340">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-340">**Output:**</span></span>

![Tutar İpucu: Gerçek ve tahmin edilen](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="4ea75-342">Bir GBT regresyon modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ea75-342">Create a GBT regression model</span></span>
<span data-ttu-id="4ea75-343">Merhaba Spark ML kullanarak bir GBT regresyon modeli oluşturma `GBTRegressor()` işlev ve test verileri hello modeli değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="4ea75-344">[Gradyan boosted ağaçları](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) olan karar ağaçları ensembles.</span><span class="sxs-lookup"><span data-stu-id="4ea75-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="4ea75-345">GBTs tren karar tekrarlayarak toominimize kaybı işlevi ağaçları.</span><span class="sxs-lookup"><span data-stu-id="4ea75-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="4ea75-346">GBTs regresyon ve sınıflandırma için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="4ea75-347">Bunlar kategorik özellikleri işleyebilir, özellik ölçeklendirme gerektirmez ve nonlinearities ve özellik etkileşimleri yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="4ea75-348">Bunları bir sınıflandırma veya çoklu sınıflar ayarını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea75-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="4ea75-349">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-349">**Output:**</span></span>

<span data-ttu-id="4ea75-350">Test R-sqr olduğu: 0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="4ea75-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="4ea75-351">En iyi duruma getirme için Gelişmiş modelleme yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="4ea75-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="4ea75-352">Bu bölümde, geliştiricilerin modeli iyileştirme için sık kullandığınız machine learning yardımcı programlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="4ea75-353">Özellikle, makine öğrenimi modellerini üç farklı yolla parametre Süpürme ve çapraz doğrulama kullanarak en iyi duruma getirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4ea75-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="4ea75-354">Tren ve doğrulama kümeleri bölünmüş hello verileri eğitim kümesinde hyper-parametre Süpürme kullanarak hello modeli iyileştirmek ve doğrulama kümesinde (doğrusal regresyon) değerlendir</span><span class="sxs-lookup"><span data-stu-id="4ea75-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="4ea75-355">Çapraz doğrulama ve hyper-Spark ML'ın CrossValidator işlevi (ikili sınıflandırma) kullanarak yerleştirmez parametresini kullanarak Hello modeli en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="4ea75-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="4ea75-356">İşlev ve parametre kümesi (doğrusal regresyon) öğrenme herhangi bir makineye özel çapraz doğrulama ve parametre Süpürme kod toouse kullanarak Hello modeli en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="4ea75-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="4ea75-357">**Çapraz doğrulama** ne kadar iyi bilinen bir veri kümesi üzerinde eğitilmiş bir model veri kümeleri üzerinde onu eğitilmedi toopredict hello özelliklerini generalize değerlendirir bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="4ea75-358">Merhaba genel Bu teknik arkasındaki bir model bilinen veri bir veri kümesinde eğitildi ve ardından hello doğruluğu kendi tahminleri, bağımsız bir veri kümesi karşı test edilmiştir olur.</span><span class="sxs-lookup"><span data-stu-id="4ea75-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="4ea75-359">Bir ortak toodivide bir veri kümesine uygulamasıdır *k*-Katlama ve hepsini şekilde hello Katlama biri dışındaki tüm hello modeli eğitmek.</span><span class="sxs-lookup"><span data-stu-id="4ea75-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="4ea75-360">**Hyper-parametre iyileştirme** kümesiyle bir ölçü bağımsız bir veri kümesi üzerinde hello algoritması'nın performansını en iyi duruma getirme genellikle hello amacı hyper-parametrelerini bir öğrenme algoritması seçme hello sorunudur.</span><span class="sxs-lookup"><span data-stu-id="4ea75-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="4ea75-361">Parametre hyper hello model eğitim yordamı dışında belirtmelisiniz bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="4ea75-362">Hyper-parametre değerleri hakkında varsayımlar hello esneklik ve hello modeli doğruluğunu etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="4ea75-363">Karar ağaçları gibi Hello derinliği ve hello ağacında bırakır sayısı istenen hyper-parametreleri, örneğin, sahip.</span><span class="sxs-lookup"><span data-stu-id="4ea75-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="4ea75-364">Destek vektör makinesi (SVM) misclassification cezası terim ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="4ea75-365">Ortak bir şekilde tooperform parametresi hyper iyileştirme toouse bir kılavuz arama olarak da bilinir bir **parametresi tarama**.</span><span class="sxs-lookup"><span data-stu-id="4ea75-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="4ea75-366">Bir kılavuz aramada ayrıntılı aramasını hello hyper-parametre alan bir öğrenme algoritması için belirtilen bir alt hello değerlerini aracılığıyla gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="4ea75-367">Çapraz doğrulama performans ölçüm toosort hello kılavuz arama algoritması tarafından üretilen hello verimle çıkışı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="4ea75-368">Çapraz doğrulama parametre hyper Süpürme kullanırsanız, bir model tootraining verileri overfitting gibi sınırı sorunları yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="4ea75-369">Bu şekilde hello modeli hello kapasite tooapply toohello genel hangi hello eğitim verileri ayıklandı veri kümesini korur.</span><span class="sxs-lookup"><span data-stu-id="4ea75-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="4ea75-370">Doğrusal regresyon modeli parametre hyper Süpürme ile en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="4ea75-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="4ea75-371">Ardından, veri eğitimi ve doğrulama ayarlar bölme, kullanım hyper-üzerinde bir eğitim yerleştirmez parametre toooptimize hello modelini ayarlamak ve doğrulama kümesinde (doğrusal regresyon) değerlendir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="4ea75-372">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-372">**Output:**</span></span>

<span data-ttu-id="4ea75-373">Test R-sqr olduğu: 0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="4ea75-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="4ea75-374">Çapraz doğrulama ve parametre hyper Süpürme kullanarak Hello ikili sınıflandırma modeli en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="4ea75-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="4ea75-375">Bu bölümde, nasıl toooptimize ikili sınıflandırma model çapraz doğrulama ve parametre hyper Süpürme kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="4ea75-376">Bu hello Spark ML kullanır `CrossValidator` işlevi.</span><span class="sxs-lookup"><span data-stu-id="4ea75-376">This uses hello Spark ML `CrossValidator` function.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="4ea75-377">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-377">**Output:**</span></span>

<span data-ttu-id="4ea75-378">Zaman toorun hello hücre: 33 saniye.</span><span class="sxs-lookup"><span data-stu-id="4ea75-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="4ea75-379">Özel çapraz doğrulama ve parametre Süpürme kod kullanarak Hello doğrusal regresyon modeli en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="4ea75-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="4ea75-380">Ardından, özel kod kullanarak hello modeli iyileştirmek ve en yüksek doğruluk hello ölçütünü kullanarak hello en iyi modeli parametreleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4ea75-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="4ea75-381">Ardından, hello son model oluşturun, test verileri hello modeli değerlendirin ve Blob depolama alanına hello modeli kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="4ea75-382">Son olarak, hello modeli yüklemek için test verileri puan ve doğruluk değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="4ea75-383">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="4ea75-383">**Output:**</span></span>

<span data-ttu-id="4ea75-384">Zaman toorun hello hücre: 61 saniye.</span><span class="sxs-lookup"><span data-stu-id="4ea75-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="4ea75-385">Spark yerleşik makine öğrenimi modellerini Scala ile otomatik olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="4ea75-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="4ea75-386">Azure'da hello veri bilimi işlemi oluşturan hello görevleri rehberlik konuları genel bakış için bkz: [takım veri bilimi işlemi](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="4ea75-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="4ea75-387">[Ekip veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md) hello adımları hello takım veri bilimi işlemi belirli senaryoları için gösteren diğer uçtan uca talimatlara açıklar.</span><span class="sxs-lookup"><span data-stu-id="4ea75-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="4ea75-388">Hello izlenecek yollar da nasıl toocombine bulut göstermek ve şirket içi araçları ve akıllı bir uygulama bir iş akışı veya ardışık düzen toocreate Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="4ea75-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="4ea75-389">[Spark yerleşik machine learning modellerini puan](machine-learning-data-science-spark-model-consumption.md) nasıl toouse Scala kod tooautomatically yükleyin ve yeni veri kümeleri ile Spark oluşturulmuş ve Azure Blob depolama alanına kaydedildi machine learning modellerini puan gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ea75-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="4ea75-390">Var. hello yönergelerini izleyin ve yalnızca bu makalede otomatik tüketimi için Scala koduyla hello Python kodu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4ea75-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

