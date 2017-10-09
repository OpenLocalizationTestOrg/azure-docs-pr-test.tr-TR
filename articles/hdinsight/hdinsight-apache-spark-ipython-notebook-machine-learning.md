---
title: "Azure Hdınsight uygulamaları öğrenme aaaBuild Apache Spark machine | Microsoft Docs"
description: "Adım adım yönergeler Jupyter Not Defteri kullanarak nasıl uygulama Hdınsight Spark üzerinde öğrenme toobuild Apache Spark makine kümeleri"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="c3d46-103">Azure hdınsight'ta Apache Spark machine learning uygulamaları derleme</span><span class="sxs-lookup"><span data-stu-id="c3d46-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="c3d46-104">Nasıl toobuild bir Spark kullanarak Apache Spark machine learning uygulama küme Hdınsight'ta öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c3d46-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="c3d46-105">Bu makalede nasıl toouse Jupyter not defteri ile Merhaba küme toobuild kullanılabilir hello ve bu uygulamayı test gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c3d46-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="c3d46-106">Merhaba uygulaması varsayılan olarak tüm kümelerde kullanılabilir hello örnek HVAC.csv verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3d46-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="c3d46-107">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="c3d46-107">**Prerequisites:**</span></span>

<span data-ttu-id="c3d46-108">Merhaba şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c3d46-108">You must have hello following:</span></span>

* <span data-ttu-id="c3d46-109">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="c3d46-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="c3d46-110">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c3d46-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="c3d46-111"><a name="data"></a>Merhaba veri kümesi anlama</span><span class="sxs-lookup"><span data-stu-id="c3d46-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="c3d46-112">Bize hello uygulaması oluşturmaya başlamadan önce biz Merhaba uygulaması gerçekleştiririz analiz hello tür hello verileri yapı ve hello verilerin hello yapısını anlayın.</span><span class="sxs-lookup"><span data-stu-id="c3d46-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="c3d46-113">Bu makalede, kullandığımız hello örnek **HVAC.csv** hello hello Hdınsight kümesi ile ilişkili Azure depolama hesabı kullanılabilir veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="c3d46-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="c3d46-114">Merhaba dosya altındadır Hello depolama hesabında **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="c3d46-115">İndirip hello CSV dosyası tooget hello verilerin bir anlık görüntüsünü açın.</span><span class="sxs-lookup"><span data-stu-id="c3d46-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="c3d46-116">![Spark machine learning örnek için kullanılan verilerin anlık görüntüsünü](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Spark machine learning örnek için kullanılan verilerin anlık görüntüsünü")</span><span class="sxs-lookup"><span data-stu-id="c3d46-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="c3d46-117">Merhaba verileri hello hedef sıcaklık ve hello gerçek HVAC sistemleri yüklü olan bir bina sıcaklığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3d46-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="c3d46-118">Merhaba varsayalım **sistem** sütunu temsil eder hello sistem Kimliğini ve hello **SystemAge** sütun hello hello HVAC sistem hello yapı yerinde açıldı yıl sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c3d46-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="c3d46-119">Bir yapı sistem Kimliğini ve sistem yaş verilen hello hedef sıcaklık üzerinde hotter veya colder tabanlı gerektirmeyeceğini bu verileri toopredict kullanırız.</span><span class="sxs-lookup"><span data-stu-id="c3d46-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="c3d46-120"><a name="app"></a>Spark Mllib'i kullanarak Spark machine learning uygulaması yazma</span><span class="sxs-lookup"><span data-stu-id="c3d46-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="c3d46-121">Bu uygulamada Spark ML ardışık düzen tooperform bir belge sınıflandırma kullanırız.</span><span class="sxs-lookup"><span data-stu-id="c3d46-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="c3d46-122">Merhaba ardışık düzeninde biz sözcüklere hello belgeyi bölme, bir sayısal özellik vektör hello sözcükleri dönüştürme ve son olarak hello özelliği vektörlerinin ve etiketleri kullanarak bir tahmin modeli yapı.</span><span class="sxs-lookup"><span data-stu-id="c3d46-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="c3d46-123">Aşağıdaki adımları toocreate Merhaba uygulaması hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c3d46-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="c3d46-124">Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3d46-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="c3d46-125">Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="c3d46-126">Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="c3d46-127">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="c3d46-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3d46-128">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="c3d46-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="c3d46-129">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="c3d46-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="c3d46-130">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3d46-130">Create a new notebook.</span></span> <span data-ttu-id="c3d46-131">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c3d46-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="c3d46-132">![Spark machine learning örneğin Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Spark machine learning örneğin Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="c3d46-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="c3d46-133">Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile.</span><span class="sxs-lookup"><span data-stu-id="c3d46-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="c3d46-134">Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="c3d46-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="c3d46-135">![Spark machine learning örnek için bir not defteri ad](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Spark machine learning örneğin Not defteri adını belirtin")</span><span class="sxs-lookup"><span data-stu-id="c3d46-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="c3d46-136">Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c3d46-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="c3d46-137">Merhaba birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları hello otomatik olarak sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c3d46-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="c3d46-138">Bu senaryo için gerekli olan hello türleri içeri aktararak işleme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3d46-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="c3d46-139">Boş bir hücre parçacığında aşağıdaki hello yapıştırın ve tuşuna basın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. <span data-ttu-id="c3d46-140">Şimdi hello verileri (hvac.csv) yüklemek, bunu ayrıştırabilir ve gerekir tootrain hello modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3d46-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="c3d46-141">Bunun için hello gerçek hello bina sıcaklığını hello hedef sıcaklık büyük olup olmadığını denetler bir işlev tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c3d46-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="c3d46-142">Merhaba gerçek sıcaklık büyük hello yapı hello değeri tarafından belirtilen hareketli, ise, **1.0**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="c3d46-143">Merhaba gerçek sıcaklık küçük hello yapı hello değeri tarafından belirtilen soğuk, ise, **0,0**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="c3d46-144">Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="c3d46-145">Üç aşamadan oluşur hello Spark machine learning ardışık düzenini yapılandırın: belirteç Oluşturucu, hashingTF ve lr.</span><span class="sxs-lookup"><span data-stu-id="c3d46-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="c3d46-146">İşlem hattı nedir ve bakın nasıl çalıştığı hakkında daha fazla bilgi için <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning ardışık</a>.</span><span class="sxs-lookup"><span data-stu-id="c3d46-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="c3d46-147">Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="c3d46-148">Uygun hello ardışık düzen toohello eğitim belgesi.</span><span class="sxs-lookup"><span data-stu-id="c3d46-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="c3d46-149">Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="c3d46-150">Merhaba eğitim belge toocheckpoint hello uygulamayla ilerleme durumunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c3d46-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="c3d46-151">Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="c3d46-152">Bu hello çıkış benzer toohello aşağıdaki vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c3d46-152">This should give hello output similar toohello following:</span></span>
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    <span data-ttu-id="c3d46-153">Geri dönün ve hello çıktı hello ham CSV dosyası karşı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c3d46-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="c3d46-154">Örneğin, bu veri hello ilk satır hello CSV dosyası sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c3d46-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="c3d46-155">![Çıkış Spark machine learning örnek için anlık görüntü verileri](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Spark machine learning örnek için çıktı veri anlık görüntüsü")</span><span class="sxs-lookup"><span data-stu-id="c3d46-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="c3d46-156">Merhaba yapı öneren hello hedef sıcaklık soğuk küçüktür hello gerçek sıcaklık nasıl olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c3d46-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="c3d46-157">Bu nedenle hello eğitim çıktısında değeri hello **etiket** hello ilk satırıdır **0,0**, yani hello yapı etkin değil.</span><span class="sxs-lookup"><span data-stu-id="c3d46-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="c3d46-158">Veri kümesi toorun hello eğitilen model karşı hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="c3d46-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="c3d46-159">toodo bu nedenle, biz bir sistem Kimliğini ve sistem yaş geçip geçmeyeceğini (olarak gösterilen **SystemInfo** hello eğitim çıkışı), ve hello modeli tahmin olup hello hotter (gösterilir tarafından 1.0) Bu sistem Kimliğini ve sistem geçerlilik süresi ile oluşturduğunuz veya için ( 0,0 tarafından gösterilen).</span><span class="sxs-lookup"><span data-stu-id="c3d46-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="c3d46-160">Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="c3d46-161">Son olarak, hello test verileri üzerindeki tahminlerde.</span><span class="sxs-lookup"><span data-stu-id="c3d46-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="c3d46-162">Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="c3d46-163">Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c3d46-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="c3d46-164">İlk satırdaki Hello hello tahmin içinde kimliği 20 ve 25 yıllık sistem geçerlilik süresi ile bir HVAC sistemi için hello yapı etkin olacağını görebilirsiniz (**tahmin = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="c3d46-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="c3d46-165">Merhaba ilk değer DenseVector (0.49999) için toohello tahmin 0,0 karşılık gelir ve hello ikinci değer (0.5001) toohello tahmin 1.0 karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="c3d46-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="c3d46-166">Merhaba çıktısında hello ikinci değer yalnızca fazladır daha yüksek olmasına rağmen hello modelini gösteren **tahmin = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="c3d46-167">Merhaba uygulaması çalıştıran bitirdikten sonra kapatma hello not defteri toorelease hello kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3d46-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="c3d46-168">toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.</span><span class="sxs-lookup"><span data-stu-id="c3d46-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="c3d46-169">Bu işlem kapatma ve Kapat hello dizüstü.</span><span class="sxs-lookup"><span data-stu-id="c3d46-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="c3d46-170"><a name="anaconda"></a>Anaconda scikit kullanın-Spark machine learning için kitaplık öğrenin</span><span class="sxs-lookup"><span data-stu-id="c3d46-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="c3d46-171">Hdınsight'ta Apache Spark kümeleri Anaconda kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="c3d46-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="c3d46-172">Bu da hello içerir **scikit-öğrenin** machine learning için kitaplık.</span><span class="sxs-lookup"><span data-stu-id="c3d46-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="c3d46-173">Merhaba kitaplığı toobuild örnek uygulamalardan doğrudan Jupyter not defteri kullanabileceğiniz çeşitli veri kümeleri de içerir.</span><span class="sxs-lookup"><span data-stu-id="c3d46-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="c3d46-174">Scikit kullanma örnekleri hello için-kitaplık bilgi [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="c3d46-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="c3d46-175"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c3d46-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="c3d46-176">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="c3d46-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c3d46-177">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="c3d46-177">Scenarios</span></span>
* [<span data-ttu-id="c3d46-178">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="c3d46-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c3d46-179">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="c3d46-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c3d46-180">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="c3d46-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c3d46-181">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="c3d46-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c3d46-182">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c3d46-182">Create and run applications</span></span>
* [<span data-ttu-id="c3d46-183">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3d46-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c3d46-184">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c3d46-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c3d46-185">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="c3d46-185">Tools and extensions</span></span>
* [<span data-ttu-id="c3d46-186">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="c3d46-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c3d46-187">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="c3d46-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c3d46-188">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="c3d46-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c3d46-189">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="c3d46-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c3d46-190">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="c3d46-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c3d46-191">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="c3d46-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c3d46-192">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="c3d46-192">Manage resources</span></span>
* [<span data-ttu-id="c3d46-193">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="c3d46-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c3d46-194">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="c3d46-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
