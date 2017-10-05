---
title: "Azure hdınsight'ta Apache Spark machine learning uygulamaları derleme | Microsoft Docs"
description: "Apache Spark machine learning uygulama oluşturmak adım adım yönergeler Jupyter Not Defteri kullanarak Spark Hdınsight kümeleri"
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
ms.openlocfilehash: 158ade4612104020e0231794e7123ea5cad6c459
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="b4749-103">Azure hdınsight'ta Apache Spark machine learning uygulamaları derleme</span><span class="sxs-lookup"><span data-stu-id="b4749-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="b4749-104">Hdınsight'ta Spark kümesi kullanarak uygulama öğrenme bir Apache Spark makine oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b4749-104">Learn how to build an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="b4749-105">Bu makalede kullanılabilir Jupyter not defteri ile küme oluşturmak ve bu uygulamayı test için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b4749-105">This article shows how to use the Jupyter notebook available with the cluster to build and test this application.</span></span> <span data-ttu-id="b4749-106">Uygulama, varsayılan olarak tüm kümelerde kullanılabilir örnek HVAC.csv verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="b4749-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="b4749-107">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="b4749-107">**Prerequisites:**</span></span>

<span data-ttu-id="b4749-108">Aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b4749-108">You must have the following:</span></span>

* <span data-ttu-id="b4749-109">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="b4749-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b4749-110">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b4749-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="b4749-111"><a name="data"></a>Veri kümesi anlama</span><span class="sxs-lookup"><span data-stu-id="b4749-111"><a name="data"></a>Understand the data set</span></span>
<span data-ttu-id="b4749-112">Uygulama oluşturmaya başlamadan önce bize, biz uygulama gerçekleştiririz analiz türünü verileri yapı ve verilerin yapısını anlayın.</span><span class="sxs-lookup"><span data-stu-id="b4749-112">Before we start building the application, let us understand the structure of the data for which we build the application and the kind of analysis we will do on the data.</span></span> 

<span data-ttu-id="b4749-113">Bu makaledeki örnek kullanırız **HVAC.csv** Hdınsight kümesi ile ilişkili Azure depolama hesabı kullanılabilir veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="b4749-113">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span></span> <span data-ttu-id="b4749-114">Depolama hesabında dosya altındadır **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="b4749-114">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="b4749-115">Karşıdan yükle ve verilerin bir anlık görüntüsünü almak için CSV dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="b4749-115">Download and open the CSV file to get a snapshot of the data.</span></span>  

<span data-ttu-id="b4749-116">![Spark machine learning örnek için kullanılan verilerin anlık görüntüsünü](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Spark machine learning örnek için kullanılan verilerin anlık görüntüsünü")</span><span class="sxs-lookup"><span data-stu-id="b4749-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="b4749-117">Verileri hedef sıcaklık ve gerçek HVAC sistemleri yüklü olan bir bina sıcaklığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4749-117">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="b4749-118">Varsayalım **sistem** sütun sistem Kimliğini temsil eder ve **SystemAge** sütun HVAC sistem yapı yerinde açıldı yıl sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b4749-118">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span>

<span data-ttu-id="b4749-119">Bir yapı sistem Kimliğini ve sistem yaş verilen hedef sıcaklık hotter veya colder tabanlı olup olmayacağını tahmin etmek için bu verileri kullanırız.</span><span class="sxs-lookup"><span data-stu-id="b4749-119">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="b4749-120"><a name="app"></a>Spark Mllib'i kullanarak Spark machine learning uygulaması yazma</span><span class="sxs-lookup"><span data-stu-id="b4749-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="b4749-121">Bu uygulamada bir belge sınıflandırması yapmak için Spark ML işlem hattı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4749-121">In this application we use a Spark ML pipeline to perform a document classification.</span></span> <span data-ttu-id="b4749-122">Ardışık düzeninde biz sözcüklere belgeyi bölme, bir sayısal özellik vektör sözcükleri dönüştürme ve son olarak özellik vektörlerinin ve etiketleri kullanarak bir tahmin modeli yapı.</span><span class="sxs-lookup"><span data-stu-id="b4749-122">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="b4749-123">Uygulama oluşturmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b4749-123">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="b4749-124">[Azure Portal](https://portal.azure.com/)’daki başlangıç panosunda Spark kümenizin kutucuğuna tıklayın (başlangıç panosuna sabitlediyseniz).</span><span class="sxs-lookup"><span data-stu-id="b4749-124">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="b4749-125">Ayrıca **Browse All (Tümüne Gözat)** > **HDInsight Clusters (HDInsight Kümeleri)** altından kümenize gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4749-125">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="b4749-126">Spark kümesi dikey penceresinden **Küme Panosu**’na ve ardından **Jupyter Notebook**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4749-126">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="b4749-127">İstenirse, küme için yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="b4749-127">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b4749-128">Aşağıdaki URL’yi tarayıcınızda açarak da Jupyter Notebook’a ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4749-128">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="b4749-129">**CLUSTERNAME** değerini kümenizin adıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b4749-129">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="b4749-130">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b4749-130">Create a new notebook.</span></span> <span data-ttu-id="b4749-131">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4749-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="b4749-132">![Spark machine learning örneğin Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Spark machine learning örneğin Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="b4749-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="b4749-133">Yeni bir not defteri oluşturulur ve Untitled.pynb adı ile açılır.</span><span class="sxs-lookup"><span data-stu-id="b4749-133">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="b4749-134">Üstteki not defteri adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="b4749-134">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="b4749-135">![Spark machine learning örnek için bir not defteri ad](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Spark machine learning örneğin Not defteri adını belirtin")</span><span class="sxs-lookup"><span data-stu-id="b4749-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="b4749-136">PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için açıkça bir bağlam oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b4749-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="b4749-137">Birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b4749-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="b4749-138">Bu senaryo için gereken türleri içeri aktararak işleme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4749-138">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="b4749-139">Boş bir hücreye aşağıdaki kod parçacığını yapıştırın ve sonra basın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4749-139">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="b4749-140">Şimdi (hvac.csv) veri yükleme, bunu ayrıştırabilir ve bunu modeli eğitmek için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4749-140">You must now load the data (hvac.csv), parse it, and use it to train the model.</span></span> <span data-ttu-id="b4749-141">Bu, gerçek bina sıcaklığını hedef sıcaklık büyük olup olmadığını denetler bir işlev tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b4749-141">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span></span> <span data-ttu-id="b4749-142">Gerçek sıcaklık büyükse, yapı değeri tarafından belirtilen hareketli, **1.0**.</span><span class="sxs-lookup"><span data-stu-id="b4749-142">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="b4749-143">Gerçek sıcaklık küçük yapı değeri tarafından belirtilen soğuk, ise, **0,0**.</span><span class="sxs-lookup"><span data-stu-id="b4749-143">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span></span> 
   
    <span data-ttu-id="b4749-144">Aşağıdaki kod parçacığını yapıştırın bir boş bir hücre ve tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4749-144">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List the structure of data for better understanding. Because the data will be
        # loaded as an array, this structure makes it easy to understand what each element
        # in the array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses the raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load the raw HVAC.csv file, parse it using the function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="b4749-145">Üç aşamadan oluşur Spark machine learning ardışık düzenini yapılandırın: belirteç Oluşturucu, hashingTF ve lr.</span><span class="sxs-lookup"><span data-stu-id="b4749-145">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="b4749-146">İşlem hattı nedir ve bakın nasıl çalıştığı hakkında daha fazla bilgi için <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning ardışık</a>.</span><span class="sxs-lookup"><span data-stu-id="b4749-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="b4749-147">Aşağıdaki kod parçacığını yapıştırın bir boş bir hücre ve tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4749-147">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="b4749-148">Ardışık Düzen eğitim belgeye uygun.</span><span class="sxs-lookup"><span data-stu-id="b4749-148">Fit the pipeline to the training document.</span></span> <span data-ttu-id="b4749-149">Aşağıdaki kod parçacığını yapıştırın bir boş bir hücre ve tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4749-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="b4749-150">Denetim noktası eğitim belgeye uygulamayla ilerleme durumunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b4749-150">Verify the training document to checkpoint your progress with the application.</span></span> <span data-ttu-id="b4749-151">Aşağıdaki kod parçacığını yapıştırın bir boş bir hücre ve tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4749-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="b4749-152">Bu, aşağıdakine benzer bir çıktı vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="b4749-152">This should give the output similar to the following:</span></span>
   
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

    <span data-ttu-id="b4749-153">Geri dönün ve çıktı ham CSV dosyası karşı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b4749-153">Go back and verify the output against the raw CSV file.</span></span> <span data-ttu-id="b4749-154">Örneğin, CSV dosyasının ilk satırı bu verileri vardır:</span><span class="sxs-lookup"><span data-stu-id="b4749-154">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="b4749-155">![Çıkış Spark machine learning örnek için anlık görüntü verileri](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Spark machine learning örnek için çıktı veri anlık görüntüsü")</span><span class="sxs-lookup"><span data-stu-id="b4749-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="b4749-156">Nasıl gerçek sıcaklık yapı soğuk öneren hedef sıcaklık değerinden olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b4749-156">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="b4749-157">Bu nedenle çıktı, eğitim değeri **etiket** ilk sırada **0,0**, yapı başka bir deyişle, etkin değil.</span><span class="sxs-lookup"><span data-stu-id="b4749-157">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

1. <span data-ttu-id="b4749-158">Bir veri kümesi ve eğitilen modele karşı çalıştırmak için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="b4749-158">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="b4749-159">Bunu yapmak için kimliğinizi bir sistem Kimliğini ve sistem yaş geçip geçmeyeceğini (olarak gösterilen **SystemInfo** eğitim çıkışı), ve model oluşturma, sistem Kimliğini ve sistem geçerlilik süresi ile hotter olup tahmin etmek (1.0 tarafından gösterilen) veya daha soğuk (belirtilmiştir 0,0).</span><span class="sxs-lookup"><span data-stu-id="b4749-159">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="b4749-160">Aşağıdaki kod parçacığını yapıştırın bir boş bir hücre ve tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4749-160">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="b4749-161">Son olarak, test verileri üzerindeki tahminlerde.</span><span class="sxs-lookup"><span data-stu-id="b4749-161">Finally, make predictions on the test data.</span></span> <span data-ttu-id="b4749-162">Aşağıdaki kod parçacığını yapıştırın bir boş bir hücre ve tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4749-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="b4749-163">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="b4749-163">You should see an output similar to the following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="b4749-164">Tahmin ilk satırdan kimliği 20 ve 25 yıllık sistem geçerlilik süresi ile bir HVAC sistemi için yapı etkin olacağını görebilirsiniz (**tahmin = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="b4749-164">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="b4749-165">DenseVector (0.49999) ilk değeri 0,0 tahmin karşılık gelir ve ikinci değer (0.5001) 1.0 tahmin karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="b4749-165">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="b4749-166">Çıktıda ikinci değer yalnızca fazladır daha yüksek olmasına rağmen modelini gösteren **tahmin = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="b4749-166">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="b4749-167">Uygulamayı çalıştırmayı tamamladıktan sonra kaynakları serbest bırakmak için not defterini kapatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4749-167">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="b4749-168">Bunu yapmak için not defterindeki **Dosya** menüsünde **Kapat ve Durdur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4749-168">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="b4749-169">Bunun yapılması not defterini kapatır.</span><span class="sxs-lookup"><span data-stu-id="b4749-169">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="b4749-170"><a name="anaconda"></a>Anaconda scikit kullanın-Spark machine learning için kitaplık öğrenin</span><span class="sxs-lookup"><span data-stu-id="b4749-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="b4749-171">Hdınsight'ta Apache Spark kümeleri Anaconda kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="b4749-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="b4749-172">Bu da içerir **scikit-öğrenin** machine learning için kitaplık.</span><span class="sxs-lookup"><span data-stu-id="b4749-172">This also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="b4749-173">Kitaplık Ayrıca örnek uygulamalardan doğrudan Jupyter not defteri oluşturmak için kullanabileceğiniz çeşitli veri kümelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b4749-173">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="b4749-174">Scikit kullanma ile ilgili örnekler-kitaplık bilgi [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="b4749-174">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="b4749-175"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b4749-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b4749-176">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="b4749-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b4749-177">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="b4749-177">Scenarios</span></span>
* [<span data-ttu-id="b4749-178">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="b4749-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b4749-179">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="b4749-179">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b4749-180">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="b4749-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b4749-181">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="b4749-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b4749-182">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b4749-182">Create and run applications</span></span>
* [<span data-ttu-id="b4749-183">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4749-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b4749-184">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b4749-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b4749-185">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="b4749-185">Tools and extensions</span></span>
* [<span data-ttu-id="b4749-186">Spark Scala uygulamaları oluşturmak ve göndermek amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="b4749-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b4749-187">Spark uygulamalarında uzaktan hata ayıklamak amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="b4749-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b4749-188">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="b4749-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b4749-189">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="b4749-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b4749-190">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="b4749-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b4749-191">Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="b4749-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b4749-192">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="b4749-192">Manage resources</span></span>
* [<span data-ttu-id="b4749-193">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b4749-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b4749-194">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="b4749-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
