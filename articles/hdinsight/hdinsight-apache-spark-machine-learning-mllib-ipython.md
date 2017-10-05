---
title: "Spark Mllib'i hdınsight'ta - Azure Machine learning örnekle | Microsoft Docs"
description: "Spark Mllib'i Lojistik regresyon aracılığıyla sınıflandırmasını kullanan bir veri kümesi analiz bir makine öğrenme uygulaması oluşturmak için nasıl kullanılacağını öğrenin."
keywords: "spark machine Learning, spark machine learning örneği"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: e563d4f51c9e27b20df47eca6d3eb00ac79e854f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="6ff36-104">Machine learning uygulama oluşturmak ve bir veri kümesi analiz etmek için Spark Mllib'i kullanın</span><span class="sxs-lookup"><span data-stu-id="6ff36-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="6ff36-105">Spark kullanmayı öğrenin **Mllib'i** açık bir veri kümesi üzerinde basit Tahmine dayalı analiz yapmak için uygulama öğrenme bir makine oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="6ff36-105">Learn how to use Spark **MLlib** to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="6ff36-106">Bu örnek kitaplıkları öğrenme Spark'ın yerleşik makineden kullanır *sınıflandırma* Lojistik regresyon aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="6ff36-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="6ff36-107">Bu örnek, Hdınsight'ta oluşturma (Linux) Spark kümesinde Jupyter not defteri olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="6ff36-108">Not Defteri deneyimi Python parçacıkları dizüstü çalıştırmadan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ff36-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="6ff36-109">Gelen öğretici bir not defteri içinde takip etmek için bir Spark kümesi oluşturma ve Jupyter not defteri başlatın (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="6ff36-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="6ff36-110">Ardından, Not Defteri çalıştırın **Spark Machine Learning - yemek İnceleme verileri MLlib.ipynb kullanarak Tahmine dayalı analiz** altında **Python** klasör.</span><span class="sxs-lookup"><span data-stu-id="6ff36-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="6ff36-111">Mllib'i makine öğrenimi görevlerini uygun yardımcı programlar da dahil olmak üzere, birçok yardımcı programını yararlı sağlayan bir çekirdek Spark kitaplığıdır:</span><span class="sxs-lookup"><span data-stu-id="6ff36-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="6ff36-112">Sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="6ff36-112">Classification</span></span>
* <span data-ttu-id="6ff36-113">regresyon</span><span class="sxs-lookup"><span data-stu-id="6ff36-113">Regression</span></span>
* <span data-ttu-id="6ff36-114">Kümeleme</span><span class="sxs-lookup"><span data-stu-id="6ff36-114">Clustering</span></span>
* <span data-ttu-id="6ff36-115">Konu modelleme</span><span class="sxs-lookup"><span data-stu-id="6ff36-115">Topic modeling</span></span>
* <span data-ttu-id="6ff36-116">Tekil değer ayrıştırma (SVD) ve asıl bileşen çözümlemesi (PCA)</span><span class="sxs-lookup"><span data-stu-id="6ff36-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="6ff36-117">Test etme ve örnek istatistikleri hesaplama varsayımınızın</span><span class="sxs-lookup"><span data-stu-id="6ff36-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="6ff36-118">Sınıflandırma ve lojistik regresyon nelerdir?</span><span class="sxs-lookup"><span data-stu-id="6ff36-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="6ff36-119">*Sınıflandırma*, görev, öğrenme popüler bir makine kategoriye giriş verileri sıralama işlemidir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="6ff36-120">Sağladığınız veri girişi için "etiketleri" atayın nasıl bulmak için bir sınıflandırma algoritmasıdır işi var.</span><span class="sxs-lookup"><span data-stu-id="6ff36-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="6ff36-121">Örneğin, stok bilgilerini giriş olarak kabul eder ve iki kategoride hisse senedi böler makine öğrenme algoritmasının düşündüğünüz: satmak stoklar ve hisse tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="6ff36-122">Lojistik regresyon sınıflandırma için kullandığınız algoritmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6ff36-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="6ff36-123">Spark'ın Lojistik regresyon API için yararlıdır *ikili sınıflandırma*, veya iki gruplarının biri giriş verileri sınıflandırmaya.</span><span class="sxs-lookup"><span data-stu-id="6ff36-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="6ff36-124">Lojistik gerileme hakkında daha fazla bilgi için bkz: [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="6ff36-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="6ff36-125">Özet olarak, üreten Lojistik regresyon sürecinin bir *Lojistik işlevi* bir giriş vektörü bir grup veya diğer ait olasılık tahmin etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="6ff36-126">Tahmine dayalı analiz örnek yemek İnceleme verileri</span><span class="sxs-lookup"><span data-stu-id="6ff36-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="6ff36-127">Bu örnekte, Spark yemek İnceleme veriler üzerinde bazı Tahmine dayalı analiz gerçekleştirmek için kullandığınız (**Food_Inspections1.csv**), edinilen aracılığıyla [Şehir, Chicago veri portalı](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="6ff36-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="6ff36-128">Bu veri kümesi her oluşturulması, (varsa) bulunan ihlalleri ve İnceleme sonuçlarını hakkında bilgiler dahil olmak üzere Chicago'da gerçekleştirildi yemek kurma incelemeleri hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="6ff36-129">CSV veri dosyası zaten konumundaki küme ile ilişkilendirilmiş depolama hesabına kullanılabilir **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="6ff36-130">Aşağıdaki adımları geçti veya kaldı yemek İnceleme için neler görmek için bir model geliştirin.</span><span class="sxs-lookup"><span data-stu-id="6ff36-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="6ff36-131">Spark MMLib machine learning uygulama oluşturmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="6ff36-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="6ff36-132">[Azure portalındaki](https://portal.azure.com/) başlangıç panosunda Spark kümenizin kutucuğuna tıklayın (başlangıç panosuna sabitlediyseniz).</span><span class="sxs-lookup"><span data-stu-id="6ff36-132">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="6ff36-133">Ayrıca **Browse All (Tümüne Gözat)** > **HDInsight Clusters (HDInsight Kümeleri)** altından kümenize gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-133">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="6ff36-134">Spark kümesi dikey penceresinden **Küme Panosu**’na ve ardından **Jupyter Notebook**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6ff36-134">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="6ff36-135">İstenirse, küme için yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="6ff36-135">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6ff36-136">Aşağıdaki URL’yi tarayıcınızda açarak da Jupyter Notebook’a ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-136">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="6ff36-137">**CLUSTERNAME** değerini kümenizin adıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6ff36-137">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="6ff36-138">Bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ff36-138">Create a notebook.</span></span> <span data-ttu-id="6ff36-139">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6ff36-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="6ff36-140">![Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "yeni bir Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="6ff36-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="6ff36-141">Yeni bir not defteri oluşturulur ve Untitled.pynb adı ile açılır.</span><span class="sxs-lookup"><span data-stu-id="6ff36-141">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="6ff36-142">Üstteki not defteri adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="6ff36-142">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="6ff36-143">![Not defteri adını belirtme](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Not defteri adını belirtme")</span><span class="sxs-lookup"><span data-stu-id="6ff36-143">![Provide a name for the notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="6ff36-144">PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için açıkça bir bağlam oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6ff36-144">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="6ff36-145">Birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6ff36-145">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="6ff36-146">Uygulamanın bu senaryo için gereken türleri içeri aktararak öğrenme makinenizi oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-146">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="6ff36-147">Bunu yapmak için imleci hücre ve tuşuna koyun **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-147">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="6ff36-148">Bir giriş dataframe oluşturun</span><span class="sxs-lookup"><span data-stu-id="6ff36-148">Construct an input dataframe</span></span>
<span data-ttu-id="6ff36-149">Biz kullanabilirsiniz `sqlContext` üzerinde yapılandırılmış veri dönüşümleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-149">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="6ff36-150">Örnek verileri yüklemek için ilk görev, ((**Food_Inspections1.csv**)) bir Spark SQL içine *dataframe*.</span><span class="sxs-lookup"><span data-stu-id="6ff36-150">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="6ff36-151">Ham verileri bir CSV biçiminde olduğundan, her satır dosyanın yapılandırılmamış metin olarak belleğe istek için Spark bağlam kullanmamız gerekiyor; Ardından, her satırın tek tek ayrıştırmak için Python'un CSV kitaplığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ff36-151">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="6ff36-152">Şimdi CSV dosyası bir RDD sahibiz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-152">We now have the CSV file as an RDD.</span></span>  <span data-ttu-id="6ff36-153">Veri ve şema anlamak için bir satır RDD alıyoruz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-153">To understand the schema of the data, we retrieve one row from the RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="6ff36-154">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-154">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="6ff36-155">Önceki çıkış bize giriş dosyası şeması hakkında bir fikir verir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-155">The preceding output gives us an idea of the schema of the input file.</span></span> <span data-ttu-id="6ff36-156">Her kuruluş, kurma, adresini, incelemeleri başka şeylerin konumu ve veri türü adını içerir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-156">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="6ff36-157">Şimdi bizim Tahmine dayalı analiz için yararlı olan ve ardından geçici bir tablo oluşturmak için kullanırız bir dataframe Grup sonuçları birkaç sütunları seçin.</span><span class="sxs-lookup"><span data-stu-id="6ff36-157">Let's select a few columns that are useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="6ff36-158">Şimdi sahip olduğumuz bir *dataframe*, `df` üzerinde biz gerçekleştirebilir bizim çözümleme.</span><span class="sxs-lookup"><span data-stu-id="6ff36-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="6ff36-159">Ayrıca bir geçici tablo çağrı sahibiz **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="6ff36-160">Dört sütun dataframe ilgi dahil ettiğiniz: **kimliği**, **adı**, **sonuçları**, ve **ihlalleri**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-160">We've included four columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="6ff36-161">Şimdi küçük bir örnek veri alın:</span><span class="sxs-lookup"><span data-stu-id="6ff36-161">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="6ff36-162">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-162">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="6ff36-163">Veri anlama</span><span class="sxs-lookup"><span data-stu-id="6ff36-163">Understand the data</span></span>
1. <span data-ttu-id="6ff36-164">Hangi veri içeren bir fikir almak başlayalım tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6ff36-164">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="6ff36-165">Örneğin, hangi farklı değerler **sonuçları** sütun?</span><span class="sxs-lookup"><span data-stu-id="6ff36-165">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="6ff36-166">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-166">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="6ff36-167">Hızlı görselleştirme bize yardımcı olabilecek neden bu sonuçlar dağıtılması hakkında.</span><span class="sxs-lookup"><span data-stu-id="6ff36-167">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="6ff36-168">Biz veriler geçici bir tablo zaten **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-168">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="6ff36-169">Tabloda sonuçları nasıl dağıtıldığını daha iyi anlamak için aşağıdaki SQL sorgusunu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-169">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="6ff36-170">`%%sql` Sihirli arkasından `-o countResultsdf` sorgu çıktısı (genellikle küme headnode) Jupyter sunucuda yerel olarak kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ff36-170">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="6ff36-171">Çıktı olarak kalıcı bir [Pandas](http://pandas.pydata.org/) belirtilen ada sahip dataframe **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-171">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="6ff36-172">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-172">You should see an output like the following:</span></span>

    <span data-ttu-id="6ff36-173">![SQL sorgu çıktısı](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL sorgu çıktısı")</span><span class="sxs-lookup"><span data-stu-id="6ff36-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="6ff36-174">`%%sql` sihrinin yanı sıra PySpark çekirdeği kullanılabilen diğer sihirler hakkında daha fazla bilgi için bkz. [Spark HDInsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="6ff36-174">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="6ff36-175">Matplotlib, veri görselleştirme oluşturmak için kullanılan bir kitaplık, bir çizim oluşturmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-175">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="6ff36-176">Çizim oluşturulması gerekir çünkü yerel olarak kalıcı gelen **countResultsdf** dataframe, kod parçacığında ile başlamalıdır `%%local` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="6ff36-176">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="6ff36-177">Bu kodu Jupyter sunucu üzerinde yerel olarak çalıştırın sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ff36-177">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="6ff36-178">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-178">You should see an output like the following:</span></span>

    <span data-ttu-id="6ff36-179">![Spark machine learning uygulama çıktı - beş farklı İnceleme sonuçlarını içeren pasta grafik](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning sonuç çıktısı")</span><span class="sxs-lookup"><span data-stu-id="6ff36-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="6ff36-180">Bir inceleme olabilir 5 ayrı sonuçları olduğunu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6ff36-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="6ff36-181">Değil bulunan iş</span><span class="sxs-lookup"><span data-stu-id="6ff36-181">Business not located</span></span>
   * <span data-ttu-id="6ff36-182">Başarısız</span><span class="sxs-lookup"><span data-stu-id="6ff36-182">Fail</span></span>
   * <span data-ttu-id="6ff36-183">Geçişi</span><span class="sxs-lookup"><span data-stu-id="6ff36-183">Pass</span></span>
   * <span data-ttu-id="6ff36-184">Koşulları içeren PSS</span><span class="sxs-lookup"><span data-stu-id="6ff36-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="6ff36-185">İş dışı</span><span class="sxs-lookup"><span data-stu-id="6ff36-185">Out of Business</span></span>

     <span data-ttu-id="6ff36-186">Bize yemek İnceleme sonucunu tahmin edebilirsiniz bir model ihlalleri verilen geliştirin.</span><span class="sxs-lookup"><span data-stu-id="6ff36-186">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="6ff36-187">Bir ikili sınıflandırma yöntemi Lojistik regresyon olduğuna göre iki kategoride verilerimizi grubuna mantıklıdır: **başarısız** ve **geçirmek**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-187">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="6ff36-188">Bir "geçirmek içeren koşullara" hala bir geçiş olduğunu biz modeli eğitmek, biz iki sonucu eşdeğer göz önünde şekilde.</span><span class="sxs-lookup"><span data-stu-id="6ff36-188">A "Pass w/ Conditions" is still a Pass, so when we train the model, we consider the two results equivalent.</span></span> <span data-ttu-id="6ff36-189">Biz bizim eğitim kümesinden kaldırmak için diğer sonuçları ("İş değil bulunan" veya "İş dışı") ile veri yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-189">Data with the other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="6ff36-190">Bu iki kategoriye sonuçları küçük bir yüzdesi yine de yapmak beri bu uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6ff36-190">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="6ff36-191">Bize bir tane var olan bizim dataframe dönüştürme (`df`) burada her denetleme temsil edildiği bir etiket ihlalleri çifti olarak yeni bir dataframe içine.</span><span class="sxs-lookup"><span data-stu-id="6ff36-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="6ff36-192">Bu örnekte bir etiketin `0.0` hata, bir etiketi temsil eder `1.0` başarı ve bir etiketi temsil eden `-1.0` bu iki yanı sıra bazı sonuçlarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6ff36-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="6ff36-193">Biz bu diğer sonuçlar yeni veri çerçevesi hesaplanırken filtreleme.</span><span class="sxs-lookup"><span data-stu-id="6ff36-193">We filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="6ff36-194">Hangi etiketli veri görülüyor görmek için şimdi bir satır alın.</span><span class="sxs-lookup"><span data-stu-id="6ff36-194">To see what the labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="6ff36-195">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-195">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="6ff36-196">Giriş dataframe Lojistik regresyon modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ff36-196">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="6ff36-197">Bizim son etiketli verileri Lojistik regresyon tarafından çözümlenebilir bir biçime dönüştürmek üzere bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-197">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="6ff36-198">Giriş Lojistik regresyon algoritması için bir dizi olmalıdır *etiket özelliği vektör çiftleri*, "özelliği vektör" vektör giriş noktasını temsil eden sayı olduğu.</span><span class="sxs-lookup"><span data-stu-id="6ff36-198">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="6ff36-199">Bu nedenle, biz yarı yapılandırılmış ve serbest metin, bir dizi bir makine kolayca anlayabileceği gerçek sayılar için birçok açıklamaları içeren "ihlalleri" sütun dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-199">So, we need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="6ff36-200">"Dizin" ayrı her sözcüğün atamak ve sağlayacak şekilde her dizinin değeri metin dizesindeki sözcüğün göreli sıklığı içeren öğrenme algoritmasının makineye vektör geçirmek için doğal dil işleme için yaklaşımı öğrenme bir standart makine bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="6ff36-200">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="6ff36-201">Mllib'i bu işlemi gerçekleştirmek için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ff36-201">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="6ff36-202">İlk olarak, "sözcükleri tek tek her dizesinde almak için her ihlalleri dize simgeleştirilecek".</span><span class="sxs-lookup"><span data-stu-id="6ff36-202">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="6ff36-203">Ardından, bir `HashingTF` her kümesi belirteçleri, bir model oluşturmak için Lojistik regresyon algoritması aktarılabilecek bir özellik vektör dönüştürmek için.</span><span class="sxs-lookup"><span data-stu-id="6ff36-203">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="6ff36-204">Biz bu adımların tümü "ardışık düzen" kullanılarak sırayla gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6ff36-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="6ff36-205">Ayrı bir test veri kümesi üzerinde modelini değerlendir</span><span class="sxs-lookup"><span data-stu-id="6ff36-205">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="6ff36-206">Çok daha önce oluşturduğumuz modeli kullanırız *tahmin* yeni incelemeleri sonuçlarını ne olacağı, gözlenen ihlalleri üzerinde temel.</span><span class="sxs-lookup"><span data-stu-id="6ff36-206">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="6ff36-207">Biz bu model dataset üzerinde eğitilmiş **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-207">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="6ff36-208">Bize ikinci bir veri kümesini kullan **Food_Inspections2.csv**, *değerlendirmek* bu modeli yeni verilere gücünü.</span><span class="sxs-lookup"><span data-stu-id="6ff36-208">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="6ff36-209">Bu ikinci veri kümesi (**Food_Inspections2.csv**) kümesi ile ilişkili varsayılan depolama kapsayıcısı içinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-209">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="6ff36-210">Aşağıdaki kod parçacığında yeni dataframe oluşturur **predictionsDf** modeli tarafından oluşturulan tahmin içerir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-210">The following snippet creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="6ff36-211">Kod parçacığını da adlı geçici bir tablo oluşturur **tahminleri** üzerinde dataframe göre.</span><span class="sxs-lookup"><span data-stu-id="6ff36-211">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="6ff36-212">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-212">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="6ff36-213">Tahminleri birini arayın.</span><span class="sxs-lookup"><span data-stu-id="6ff36-213">Look at one of the predictions.</span></span> <span data-ttu-id="6ff36-214">Bu kod parçacığında çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6ff36-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="6ff36-215">İlk giriş sınama veri kümesi için tahmini yoktur.</span><span class="sxs-lookup"><span data-stu-id="6ff36-215">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="6ff36-216">`model.transform()` Yöntemi aynı şema yeni verileri aynı dönüştürmeyi uygular ve verileri sınıflandırmak nasıl bir tahmini ulaşır.</span><span class="sxs-lookup"><span data-stu-id="6ff36-216">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="6ff36-217">Bizim tahminleri ne kadar doğru olan bir fikir almak için bazı basit istatistikleri yapabiliriz:</span><span class="sxs-lookup"><span data-stu-id="6ff36-217">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="6ff36-218">Çıktı aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="6ff36-218">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="6ff36-219">Lojistik regresyon ile Spark kullanarak bize doğru bir model ihlalleri açıklamaları İngilizce ve belirli bir iş veya geçirmek yemek İnceleme başarısız arasındaki ilişkinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ff36-219">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="6ff36-220">Görsel bir tahmin oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ff36-220">Create a visual representation of the prediction</span></span>
<span data-ttu-id="6ff36-221">Bize yardımcı olmak için son bir görsel öğe artık bu testi sonuçlarıyla ilgili nedeni oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-221">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="6ff36-222">Farklı Öngörüler ve sonuçları çıkartarak Başlat gelen **tahminleri** daha önce oluşturulan geçici bir tablo.</span><span class="sxs-lookup"><span data-stu-id="6ff36-222">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="6ff36-223">Aşağıdaki sorgularda çıktısı olarak ayrı *true_positive*, *false_positive*, *true_negative*, ve *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="6ff36-223">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="6ff36-224">Sorgularda biz görselleştirme kullanarak kapatmanız `-q` ve ayrıca çıkış kaydedin (kullanarak `-o`) ile birlikte kullanılabilir dataframes olarak `%%local` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="6ff36-224">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="6ff36-225">Son olarak, çizim kullanarak oluşturmak için aşağıdaki kod parçacığında kullanın **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="6ff36-225">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="6ff36-226">Şu çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff36-226">You should see the following output:</span></span>

    <span data-ttu-id="6ff36-227">![Uygulama çıkış - başarısız yemek incelemeleri pasta grafik yüzdelerini öğrenme Spark makine. ] (./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning sonuç çıktısı")</span><span class="sxs-lookup"><span data-stu-id="6ff36-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="6ff36-228">Geçirilen bir incelemesi için negatif bir sonuç başvuruyor ancak bu grafikte bir "pozitif" sonuç başarısız yemek İnceleme için ifade eder.</span><span class="sxs-lookup"><span data-stu-id="6ff36-228">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="6ff36-229">Not Defteri Kapat</span><span class="sxs-lookup"><span data-stu-id="6ff36-229">Shut down the notebook</span></span>
<span data-ttu-id="6ff36-230">Uygulamayı çalıştıran bitirdikten sonra kaynakları serbest bırakmak için Not Defteri kapatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ff36-230">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="6ff36-231">Bunu yapmak için not defterindeki **Dosya** menüsünde **Kapat ve Durdur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6ff36-231">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="6ff36-232">Bu kapanır ve not defterini kapatır.</span><span class="sxs-lookup"><span data-stu-id="6ff36-232">This shuts down and closes the notebook.</span></span>

## <span data-ttu-id="6ff36-233"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="6ff36-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="6ff36-234">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="6ff36-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="6ff36-235">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="6ff36-235">Scenarios</span></span>
* [<span data-ttu-id="6ff36-236">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="6ff36-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="6ff36-237">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="6ff36-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="6ff36-238">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="6ff36-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="6ff36-239">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="6ff36-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="6ff36-240">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6ff36-240">Create and run applications</span></span>
* [<span data-ttu-id="6ff36-241">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ff36-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="6ff36-242">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6ff36-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="6ff36-243">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="6ff36-243">Tools and extensions</span></span>
* [<span data-ttu-id="6ff36-244">Spark Scala uygulamaları oluşturmak ve göndermek amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisini kullanma</span><span class="sxs-lookup"><span data-stu-id="6ff36-244">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="6ff36-245">Spark uygulamalarında uzaktan hata ayıklamak amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="6ff36-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="6ff36-246">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="6ff36-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="6ff36-247">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="6ff36-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="6ff36-248">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="6ff36-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="6ff36-249">Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="6ff36-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="6ff36-250">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="6ff36-250">Manage resources</span></span>
* [<span data-ttu-id="6ff36-251">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="6ff36-251">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="6ff36-252">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="6ff36-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
