---
title: "hdınsight'ta - Azure Spark Mllib'i örnekle öğrenme aaaMachine | Microsoft Docs"
description: "Bilgi nasıl toouse Spark Mllib'i toocreate Lojistik regresyon aracılığıyla sınıflandırmasını kullanan bir veri kümesi analiz bir makine öğrenme uygulaması."
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
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="1bb49-104">Machine learning uygulama Spark Mllib'i toobuild kullanın ve bir veri kümesi analiz</span><span class="sxs-lookup"><span data-stu-id="1bb49-104">Use Spark MLlib toobuild a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="1bb49-105">Bilgi nasıl toouse Spark **Mllib'i** toocreate uygulama toodo basit Tahmine dayalı analiz açık bir veri kümesi üzerinde öğrenme makine.</span><span class="sxs-lookup"><span data-stu-id="1bb49-105">Learn how toouse Spark **MLlib** toocreate a machine learning application toodo simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="1bb49-106">Bu örnek kitaplıkları öğrenme Spark'ın yerleşik makineden kullanır *sınıflandırma* Lojistik regresyon aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="1bb49-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="1bb49-107">Bu örnek, Hdınsight'ta oluşturma (Linux) Spark kümesinde Jupyter not defteri olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="1bb49-108">Merhaba not defteri deneyimi hello Python parçacıkları hello dizüstü bilgisayarınızı kendisini çalıştırmadan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb49-108">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="1bb49-109">bir not defteri içinde toofollow hello öğretici bir Spark kümesi ve başlatma Jupyter not defteri oluşturma (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="1bb49-109">toofollow hello tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="1bb49-110">Daha sonra hello dizüstü çalıştırın **Spark Machine Learning - yemek İnceleme verileri MLlib.ipynb kullanarak Tahmine dayalı analiz** hello altında **Python** klasör.</span><span class="sxs-lookup"><span data-stu-id="1bb49-110">Then, run hello notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under hello **Python** folder.</span></span>
>
>

<span data-ttu-id="1bb49-111">Mllib'i makine öğrenimi görevlerini uygun yardımcı programlar da dahil olmak üzere, birçok yardımcı programını yararlı sağlayan bir çekirdek Spark kitaplığıdır:</span><span class="sxs-lookup"><span data-stu-id="1bb49-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="1bb49-112">Sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="1bb49-112">Classification</span></span>
* <span data-ttu-id="1bb49-113">regresyon</span><span class="sxs-lookup"><span data-stu-id="1bb49-113">Regression</span></span>
* <span data-ttu-id="1bb49-114">Kümeleme</span><span class="sxs-lookup"><span data-stu-id="1bb49-114">Clustering</span></span>
* <span data-ttu-id="1bb49-115">Konu modelleme</span><span class="sxs-lookup"><span data-stu-id="1bb49-115">Topic modeling</span></span>
* <span data-ttu-id="1bb49-116">Tekil değer ayrıştırma (SVD) ve asıl bileşen çözümlemesi (PCA)</span><span class="sxs-lookup"><span data-stu-id="1bb49-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="1bb49-117">Test etme ve örnek istatistikleri hesaplama varsayımınızın</span><span class="sxs-lookup"><span data-stu-id="1bb49-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="1bb49-118">Sınıflandırma ve lojistik regresyon nelerdir?</span><span class="sxs-lookup"><span data-stu-id="1bb49-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="1bb49-119">*Sınıflandırma*, görev, öğrenme popüler bir makine kategoriye giriş verileri sıralama hello işlemidir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-119">*Classification*, a popular machine learning task, is hello process of sorting input data into categories.</span></span> <span data-ttu-id="1bb49-120">Bu, sınıflandırma algoritması toofigure nasıl tooassign "sağladığınız tooinput veri etiketler" Merhaba iş olur.</span><span class="sxs-lookup"><span data-stu-id="1bb49-120">It is hello job of a classification algorithm toofigure out how tooassign "labels" tooinput data that you provide.</span></span> <span data-ttu-id="1bb49-121">Örneğin, giriş olarak hisse bilgilerini kabul eden bir makine öğrenme algoritmasını düşünüyorsunuz ve böler iki kategoride hisse senedi hello: satmak stoklar ve hisse tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides hello stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="1bb49-122">Lojistik regresyon sınıflandırma için kullandığınız hello algoritmasıdır.</span><span class="sxs-lookup"><span data-stu-id="1bb49-122">Logistic regression is hello algorithm that you use for classification.</span></span> <span data-ttu-id="1bb49-123">Spark'ın Lojistik regresyon API için yararlıdır *ikili sınıflandırma*, veya iki gruplarının biri giriş verileri sınıflandırmaya.</span><span class="sxs-lookup"><span data-stu-id="1bb49-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="1bb49-124">Lojistik gerileme hakkında daha fazla bilgi için bkz: [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="1bb49-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="1bb49-125">Özet olarak, lojistik regresyon hello işlemi üreten bir *Lojistik işlevi* kullanılan toopredict hello olasılık bir giriş vektörü bir grup veya hello diğer ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-125">In summary, hello process of logistic regression produces a *logistic function* that can be used toopredict hello probability that an input vector belongs in one group or hello other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="1bb49-126">Tahmine dayalı analiz örnek yemek İnceleme verileri</span><span class="sxs-lookup"><span data-stu-id="1bb49-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="1bb49-127">Bu örnekte, Spark tooperform bazı Tahmine dayalı analiz yemek İnceleme verileri kullandığınız (**Food_Inspections1.csv**) hello elde [Şehir, Chicago veri portalı](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="1bb49-127">In this example, you use Spark tooperform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through hello [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="1bb49-128">Bu veri kümesi her kurma hakkında bilgiler dahil olmak üzere Chicago'da gerçekleştirildi yemek kurma incelemeleri hakkında bilgi içerir, hello ihlalleri (varsa) bulunan ve hello İnceleme sonuçlarını hello.</span><span class="sxs-lookup"><span data-stu-id="1bb49-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, hello violations found (if any), and hello results of hello inspection.</span></span> <span data-ttu-id="1bb49-129">Merhaba CSV veri dosyası kullanılabilir zaten hello kümesine ilişkili hello depolama hesabındaki **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-129">hello CSV data file is already available in hello storage account associated with hello cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="1bb49-130">Merhaba adımları, model toosee toopass neler geliştirmek veya yemek İnceleme başarısız.</span><span class="sxs-lookup"><span data-stu-id="1bb49-130">In hello steps below, you develop a model toosee what it takes toopass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="1bb49-131">Spark MMLib machine learning uygulama oluşturmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="1bb49-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="1bb49-132">Merhaba gelen [Azure portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1bb49-132">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="1bb49-133">Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-133">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="1bb49-134">Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-134">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="1bb49-135">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="1bb49-135">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1bb49-136">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-136">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="1bb49-137">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="1bb49-137">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="1bb49-138">Bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1bb49-138">Create a notebook.</span></span> <span data-ttu-id="1bb49-139">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1bb49-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="1bb49-140">![Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "yeni bir Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="1bb49-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="1bb49-141">Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile.</span><span class="sxs-lookup"><span data-stu-id="1bb49-141">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="1bb49-142">Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="1bb49-142">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="1bb49-143">![Merhaba dizüstü bilgisayar için bir ad](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "hello dizüstü bilgisayar için bir ad sağlayın")</span><span class="sxs-lookup"><span data-stu-id="1bb49-143">![Provide a name for hello notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for hello notebook")</span></span>
1. <span data-ttu-id="1bb49-144">Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1bb49-144">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="1bb49-145">hello birinci kod hücresini çalıştırdığınızda hello Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1bb49-145">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="1bb49-146">Uygulamanın bu senaryo için gerekli hello türleri içeri aktararak öğrenme makinenizi oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb49-146">You can start building your machine learning application by importing hello types required for this scenario.</span></span> <span data-ttu-id="1bb49-147">toodo hello hücre ve tuşuna hello imleç, yerleştirin **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-147">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="1bb49-148">Bir giriş dataframe oluşturun</span><span class="sxs-lookup"><span data-stu-id="1bb49-148">Construct an input dataframe</span></span>
<span data-ttu-id="1bb49-149">Biz kullanabilirsiniz `sqlContext` yapılandırılmış veri tooperform dönüşümler.</span><span class="sxs-lookup"><span data-stu-id="1bb49-149">We can use `sqlContext` tooperform transformations on structured data.</span></span> <span data-ttu-id="1bb49-150">Merhaba ilk görevdir tooload hello örnek verileri ((**Food_Inspections1.csv**)) bir Spark SQL içine *dataframe*.</span><span class="sxs-lookup"><span data-stu-id="1bb49-150">hello first task is tooload hello sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="1bb49-151">Merhaba ham verileri bir CSV biçiminde olduğundan toouse hello Spark bağlam toopull her satırı hello dosyasının belleğe yapılandırılmamış metin olarak ihtiyacımız; Ardından, Python'un CSV kitaplığı tooparse her satır ayrı ayrı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1bb49-151">Because hello raw data is in a CSV format, we need toouse hello Spark context toopull every line of hello file into memory as unstructured text; then, you use Python's CSV library tooparse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="1bb49-152">Şimdi hello CSV dosyası bir RDD sahibiz.</span><span class="sxs-lookup"><span data-stu-id="1bb49-152">We now have hello CSV file as an RDD.</span></span>  <span data-ttu-id="1bb49-153">toounderstand hello şema hello veri RDD hello bir satır alıyoruz.</span><span class="sxs-lookup"><span data-stu-id="1bb49-153">toounderstand hello schema of hello data, we retrieve one row from hello RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="1bb49-154">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb49-154">You should see an output like hello following:</span></span>

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
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="1bb49-155">Merhaba önceki çıkış bize hello giriş dosyası hello şeması hakkında bir fikir verir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-155">hello preceding output gives us an idea of hello schema of hello input file.</span></span> <span data-ttu-id="1bb49-156">Her kuruluş, kurma, başlangıç adresi, hello veri hello incelemeleri ve başka şeylerin hello konum hello türü hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-156">It includes hello name of every establishment, hello type of establishment, hello address, hello data of hello inspections, and hello location, among other things.</span></span> <span data-ttu-id="1bb49-157">Şimdi bizim Tahmine dayalı analiz için yararlı olan ve bir dataframe, hangi biz Grup hello sonuçları sonra toocreate geçici bir tablo kullanın birkaç sütunları seçin.</span><span class="sxs-lookup"><span data-stu-id="1bb49-157">Let's select a few columns that are useful for our predictive analysis and group hello results as a dataframe, which we then use toocreate a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="1bb49-158">Şimdi sahip olduğumuz bir *dataframe*, `df` üzerinde biz gerçekleştirebilir bizim çözümleme.</span><span class="sxs-lookup"><span data-stu-id="1bb49-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="1bb49-159">Ayrıca bir geçici tablo çağrı sahibiz **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="1bb49-160">Merhaba dataframe ilgi dört sütun dahil ettiğiniz: **kimliği**, **adı**, **sonuçları**, ve **ihlalleri**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-160">We've included four columns of interest in hello dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="1bb49-161">Şimdi hello verilerin küçük bir örnek alın:</span><span class="sxs-lookup"><span data-stu-id="1bb49-161">Let's get a small sample of hello data:</span></span>

        df.show(5)

    <span data-ttu-id="1bb49-162">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb49-162">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a><span data-ttu-id="1bb49-163">Merhaba veri anlama</span><span class="sxs-lookup"><span data-stu-id="1bb49-163">Understand hello data</span></span>
1. <span data-ttu-id="1bb49-164">Tooget ne kümemize içeren bir fikir başlayalım.</span><span class="sxs-lookup"><span data-stu-id="1bb49-164">Let's start tooget a sense of what our dataset contains.</span></span> <span data-ttu-id="1bb49-165">Örneğin, ne hello farklı hello değerler **sonuçları** sütun?</span><span class="sxs-lookup"><span data-stu-id="1bb49-165">For example, what are hello different values in hello **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="1bb49-166">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb49-166">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="1bb49-167">Hızlı görselleştirme bize yardımcı olabilecek neden hello bu sonuçlar dağıtılması hakkında.</span><span class="sxs-lookup"><span data-stu-id="1bb49-167">A quick visualization can help us reason about hello distribution of these outcomes.</span></span> <span data-ttu-id="1bb49-168">Biz hello veriler geçici bir tablo zaten **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-168">We already have hello data in a temporary table **CountResults**.</span></span> <span data-ttu-id="1bb49-169">Daha iyi hello sonuçları nasıl dağıtıldığını anlamak hello tablo tooget SQL sorgusunu aşağıdaki hello çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb49-169">You can run hello following SQL query against hello table tooget a better understanding of how hello results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="1bb49-170">Merhaba `%%sql` Sihirli arkasından `-o countResultsdf` hello sorgu hello çıktısını (genellikle hello kümesinin hello headnode) hello Jupyter sunucuda yerel olarak kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb49-170">hello `%%sql` magic followed by `-o countResultsdf` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="1bb49-171">Merhaba çıkış kalıcı olarak bir [Pandas](http://pandas.pydata.org/) dataframe hello ile belirtilen adı **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-171">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **countResultsdf**.</span></span>

    <span data-ttu-id="1bb49-172">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb49-172">You should see an output like hello following:</span></span>

    <span data-ttu-id="1bb49-173">![SQL sorgu çıktısı](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL sorgu çıktısı")</span><span class="sxs-lookup"><span data-stu-id="1bb49-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="1bb49-174">Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli ve hello PySpark çekirdeği kullanılabilen diğer sihirler bkz [Spark Hdınsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="1bb49-174">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="1bb49-175">Verilerin toocreate bir çizim tooconstruct görselleştirme kitaplığı kullanılan Matplotlib de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb49-175">You can also use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="1bb49-176">Yerel olarak hello Hello çizim oluşturulması gerekir çünkü kalıcı **countResultsdf** dataframe, hello kod parçacığını hello ile başlamalıdır `%%local` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="1bb49-176">Because hello plot must be created from hello locally persisted **countResultsdf** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="1bb49-177">Bu, hello kod hello Jupyter sunucusunda yerel olarak çalıştırın sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb49-177">This ensures that hello code is run locally on hello Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="1bb49-178">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb49-178">You should see an output like hello following:</span></span>

    <span data-ttu-id="1bb49-179">![Spark machine learning uygulama çıktı - beş farklı İnceleme sonuçlarını içeren pasta grafik](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning sonuç çıktısı")</span><span class="sxs-lookup"><span data-stu-id="1bb49-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="1bb49-180">Bir inceleme olabilir 5 ayrı sonuçları olduğunu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1bb49-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="1bb49-181">Değil bulunan iş</span><span class="sxs-lookup"><span data-stu-id="1bb49-181">Business not located</span></span>
   * <span data-ttu-id="1bb49-182">Başarısız</span><span class="sxs-lookup"><span data-stu-id="1bb49-182">Fail</span></span>
   * <span data-ttu-id="1bb49-183">Geçişi</span><span class="sxs-lookup"><span data-stu-id="1bb49-183">Pass</span></span>
   * <span data-ttu-id="1bb49-184">Koşulları içeren PSS</span><span class="sxs-lookup"><span data-stu-id="1bb49-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="1bb49-185">İş dışı</span><span class="sxs-lookup"><span data-stu-id="1bb49-185">Out of Business</span></span>

     <span data-ttu-id="1bb49-186">Bize yemek inceleme, verilen hello ihlalleri hello sonucunu tahmin edebilirsiniz bir model geliştirin.</span><span class="sxs-lookup"><span data-stu-id="1bb49-186">Let us develop a model that can guess hello outcome of a food inspection, given hello violations.</span></span> <span data-ttu-id="1bb49-187">Lojistik regresyon ikili sınıflandırma yöntemi olduğundan, algılama toogroup verilerimizi iki kategoride kolaylaştırır: **başarısız** ve **geçirmek**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-187">Since logistic regression is a binary classification method, it makes sense toogroup our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="1bb49-188">Bir "geçirmek içeren koşullara" hala bir geçişi, biz hello modeli eğitmek, biz hello göz önünde şekilde iki eşdeğer sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="1bb49-188">A "Pass w/ Conditions" is still a Pass, so when we train hello model, we consider hello two results equivalent.</span></span> <span data-ttu-id="1bb49-189">Veri biz bizim eğitim kümesinden kaldırmak için hello ile diğer sonuçları ("İş değil bulunan" veya "İş dışı") kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-189">Data with hello other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="1bb49-190">Bu iki kategoriye hello sonuçları küçük bir yüzdesi yine de yapmak beri bu uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1bb49-190">This should be okay since these two categories make up a very small percentage of hello results anyway.</span></span>
1. <span data-ttu-id="1bb49-191">Bize bir tane var olan bizim dataframe dönüştürme (`df`) burada her denetleme temsil edildiği bir etiket ihlalleri çifti olarak yeni bir dataframe içine.</span><span class="sxs-lookup"><span data-stu-id="1bb49-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="1bb49-192">Bu örnekte bir etiketin `0.0` hata, bir etiketi temsil eder `1.0` başarı ve bir etiketi temsil eden `-1.0` bu iki yanı sıra bazı sonuçlarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1bb49-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="1bb49-193">Biz bu diğer sonuçlar hello yeni veri çerçevesi hesaplanırken filtreleme.</span><span class="sxs-lookup"><span data-stu-id="1bb49-193">We filter those other results out when computing hello new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="1bb49-194">toosee hangi hello gibi görünüyor veri etiketli, şimdi bir satır alın.</span><span class="sxs-lookup"><span data-stu-id="1bb49-194">toosee what hello labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="1bb49-195">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb49-195">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a><span data-ttu-id="1bb49-196">Merhaba giriş dataframe Lojistik regresyon modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="1bb49-196">Create a logistic regression model from hello input dataframe</span></span>
<span data-ttu-id="1bb49-197">Bizim son tooconvert hello Lojistik regresyon tarafından çözümlenebilir bir biçime veri etiketli bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-197">Our final task is tooconvert hello labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="1bb49-198">Merhaba giriş tooa Lojistik regresyon algoritması, bir dizi olmalıdır *etiket özelliği vektör çiftleri*hello "özelliği vektör" hello giriş noktasını temsil eden sayı vektör eder.</span><span class="sxs-lookup"><span data-stu-id="1bb49-198">hello input tooa logistic regression algorithm should be a set of *label-feature vector pairs*, where hello "feature vector" is a vector of numbers representing hello input point.</span></span> <span data-ttu-id="1bb49-199">Bu nedenle, yarı yapılandırılmış ve bir makine kolayca anlayabileceği gerçek sayılar serbest metin, tooan dizisi birçok açıklamaları içeren tooconvert hello "ihlalleri" sütun gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-199">So, we need tooconvert hello "violations" column, which is semi-structured and contains many comments in free-text, tooan array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="1bb49-200">İşleme doğal dil için bir standart machine learning yaklaşım tooassign her ayrı bir "dizin" sözcüktür ve sağlayacak şekilde hello göreli sıklığı hello metin sözcüğün her dizinin değerini içeren öğrenme algoritmasının bir vektör toohello makine geçirin dize.</span><span class="sxs-lookup"><span data-stu-id="1bb49-200">One standard machine learning approach for processing natural language is tooassign each distinct word an "index", and then pass a vector toohello machine learning algorithm such that each index's value contains hello relative frequency of that word in hello text string.</span></span>

<span data-ttu-id="1bb49-201">Mllib'i kolay bir yolu tooperform bu işlemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb49-201">MLlib provides an easy way tooperform this operation.</span></span> <span data-ttu-id="1bb49-202">İlk olarak, "her ihlalleri dize tooget hello sözcükleri tek tek her dizesinde simgeleştirilecek".</span><span class="sxs-lookup"><span data-stu-id="1bb49-202">First, "tokenize" each violations string tooget hello individual words in each string.</span></span> <span data-ttu-id="1bb49-203">Ardından, bir `HashingTF` her kümesi tooconvert belirteçler geçirilen toohello Lojistik regresyon algoritması tooconstruct sonra olabilir özelliği vektör bir model.</span><span class="sxs-lookup"><span data-stu-id="1bb49-203">Then, use a `HashingTF` tooconvert each set of tokens into a feature vector that can then be passed toohello logistic regression algorithm tooconstruct a model.</span></span> <span data-ttu-id="1bb49-204">Biz bu adımların tümü "ardışık düzen" kullanılarak sırayla gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1bb49-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a><span data-ttu-id="1bb49-205">Ayrı bir test veri kümesi üzerinde Hello modelini değerlendir</span><span class="sxs-lookup"><span data-stu-id="1bb49-205">Evaluate hello model on a separate test dataset</span></span>
<span data-ttu-id="1bb49-206">Daha önce oluşturduğumuz hello modeli kullanırız çok*tahmin* yeni incelemeleri sonuçlarını olacaktır, gözlenen hello ihlalleri üzerinde göre hangi hello.</span><span class="sxs-lookup"><span data-stu-id="1bb49-206">We can use hello model we created earlier too*predict* what hello results of new inspections will be, based on hello violations that were observed.</span></span> <span data-ttu-id="1bb49-207">Biz bu model hello dataset üzerinde eğitilmiş **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-207">We trained this model on hello dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="1bb49-208">Bize ikinci bir veri kümesini kullan **Food_Inspections2.csv**, çok*değerlendirmek* hello bu modeli yeni verilere gücünü.</span><span class="sxs-lookup"><span data-stu-id="1bb49-208">Let us use a second dataset, **Food_Inspections2.csv**, too*evaluate* hello strength of this model on new data.</span></span> <span data-ttu-id="1bb49-209">Bu ikinci veri kümesi (**Food_Inspections2.csv**) hello varsayılan depolama kapsayıcısında hello kümesi ile ilişkili olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-209">This second data set (**Food_Inspections2.csv**) should already be in hello default storage container associated with hello cluster.</span></span>

1. <span data-ttu-id="1bb49-210">Merhaba aşağıdaki kod parçacığında oluşturur Yeni dataframe **predictionsDf** hello modeli tarafından oluşturulan hello öngörü içerir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-210">hello following snippet creates a new dataframe, **predictionsDf** that contains hello prediction generated by hello model.</span></span> <span data-ttu-id="1bb49-211">Merhaba parçacığı da adlı geçici bir tablo oluşturur **tahminleri** hello dataframe üzerinde temel.</span><span class="sxs-lookup"><span data-stu-id="1bb49-211">hello snippet also creates a temporary table called **Predictions** based on hello dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="1bb49-212">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb49-212">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="1bb49-213">Merhaba tahminleri birini arayın.</span><span class="sxs-lookup"><span data-stu-id="1bb49-213">Look at one of hello predictions.</span></span> <span data-ttu-id="1bb49-214">Bu kod parçacığında çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1bb49-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="1bb49-215">Merhaba ilk giriş hello sınama veri kümesi için tahmini yoktur.</span><span class="sxs-lookup"><span data-stu-id="1bb49-215">There is a prediction for hello first entry in hello test data set.</span></span>
1. <span data-ttu-id="1bb49-216">Hello `model.transform()` yöntemi hello uygular aynı dönüştürme tooany yeni verilerle hello aynı şema ve nasıl tooclassify hello verileri, bir tahmini ulaşır.</span><span class="sxs-lookup"><span data-stu-id="1bb49-216">hello `model.transform()` method applies hello same transformation tooany new data with hello same schema, and arrive at a prediction of how tooclassify hello data.</span></span> <span data-ttu-id="1bb49-217">Bizim tahminleri ne kadar doğru olan bir fikir bazı basit istatistikleri tooget yapabiliriz:</span><span class="sxs-lookup"><span data-stu-id="1bb49-217">We can do some simple statistics tooget a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="1bb49-218">Merhaba çıktı hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="1bb49-218">hello output looks like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="1bb49-219">Lojistik regresyon ile Spark kullanarak bize hello ilişkisinin ihlalleri açıklamaları İngilizce ve belirli bir iş veya geçirmek yemek İnceleme başarısız arasında doğru bir modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb49-219">Using logistic regression with Spark gives us an accurate model of hello relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-hello-prediction"></a><span data-ttu-id="1bb49-220">Görsel bir hello tahmin oluşturma</span><span class="sxs-lookup"><span data-stu-id="1bb49-220">Create a visual representation of hello prediction</span></span>
<span data-ttu-id="1bb49-221">Biz, artık bize bu test hello sonuçları hakkında neden son görselleştirme toohelp oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb49-221">We can now construct a final visualization toohelp us reason about hello results of this test.</span></span>

1. <span data-ttu-id="1bb49-222">Merhaba farklı tahminleri çıkartarak başlatmak ve sonuçlarından hello **tahminleri** daha önce oluşturulan geçici bir tablo.</span><span class="sxs-lookup"><span data-stu-id="1bb49-222">We start by extracting hello different predictions and results from hello **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="1bb49-223">Merhaba aşağıdaki sorguları ayrı hello çıkış olarak *true_positive*, *false_positive*, *true_negative*, ve *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="1bb49-223">hello following queries separate hello output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="1bb49-224">Merhaba sorgularda aşağıdaki biz görselleştirme kullanarak kapatmanız `-q` ve ayrıca hello çıkış kaydedin (kullanarak `-o`) ile Merhaba sonra kullanılabilir dataframes olarak `%%local` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="1bb49-224">In hello queries below, we turn off visualization by using `-q` and also save hello output (by using `-o`) as dataframes that can be then used with hello `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="1bb49-225">Son olarak, aşağıdaki kod parçacığında toogenerate hello çizim kullanarak hello kullan **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-225">Finally, use hello following snippet toogenerate hello plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="1bb49-226">Çıktı aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb49-226">You should see hello following output:</span></span>

    <span data-ttu-id="1bb49-227">![Uygulama çıkış - başarısız yemek incelemeleri pasta grafik yüzdelerini öğrenme Spark makine. ] (./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning sonuç çıktısı")</span><span class="sxs-lookup"><span data-stu-id="1bb49-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="1bb49-228">Negatif bir sonuç denetleme geçirilen tooa başvuruyor ancak bu grafikte başarısız toohello yemek inceleme, sonuç "sıfırdan" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-228">In this chart, a "positive" result refers toohello failed food inspection, while a negative result refers tooa passed inspection.</span></span>

## <a name="shut-down-hello-notebook"></a><span data-ttu-id="1bb49-229">Hello dizüstü bilgisayarı</span><span class="sxs-lookup"><span data-stu-id="1bb49-229">Shut down hello notebook</span></span>
<span data-ttu-id="1bb49-230">Merhaba uygulaması çalıştıran bitirdikten sonra hello not defteri toorelease hello kaynakları kapatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb49-230">After you have finished running hello application, you should shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="1bb49-231">toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.</span><span class="sxs-lookup"><span data-stu-id="1bb49-231">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="1bb49-232">Bu kapanır ve not defterini kapatır hello.</span><span class="sxs-lookup"><span data-stu-id="1bb49-232">This shuts down and closes hello notebook.</span></span>

## <span data-ttu-id="1bb49-233"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="1bb49-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="1bb49-234">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="1bb49-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="1bb49-235">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="1bb49-235">Scenarios</span></span>
* [<span data-ttu-id="1bb49-236">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="1bb49-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="1bb49-237">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="1bb49-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="1bb49-238">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="1bb49-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="1bb49-239">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="1bb49-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="1bb49-240">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1bb49-240">Create and run applications</span></span>
* [<span data-ttu-id="1bb49-241">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="1bb49-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="1bb49-242">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1bb49-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="1bb49-243">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="1bb49-243">Tools and extensions</span></span>
* [<span data-ttu-id="1bb49-244">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="1bb49-244">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="1bb49-245">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="1bb49-245">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="1bb49-246">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="1bb49-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="1bb49-247">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="1bb49-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="1bb49-248">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="1bb49-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="1bb49-249">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="1bb49-249">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="1bb49-250">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="1bb49-250">Manage resources</span></span>
* [<span data-ttu-id="1bb49-251">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="1bb49-251">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="1bb49-252">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="1bb49-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
