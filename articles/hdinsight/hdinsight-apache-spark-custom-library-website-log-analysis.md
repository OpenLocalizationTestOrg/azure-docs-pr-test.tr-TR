---
title: "Spark - Azure Python kitaplıkları ile Web sitesi günlüklerini çözümleme | Microsoft Docs"
description: "Bu Not Azure hdınsight'taki Spark ile özel bir kitaplık kullanılarak günlük verilerini analiz etme gösterir."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2a028beb1e9eae89d32238e61b6f67c4c059a94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="f7998-103">Hdınsight'ta Spark kümesinde ile özel bir Python kitaplığı kullanarak Web sitesi günlüklerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="f7998-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="f7998-104">Bu Not hdınsight'ta Spark ile özel bir kitaplık kullanılarak günlük verilerini analiz etme gösterir.</span><span class="sxs-lookup"><span data-stu-id="f7998-104">This notebook demonstrates how to analyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="f7998-105">Adlı bir Python kitaplığı kullandığımız özel kitaplığı olan **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="f7998-105">The custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="f7998-106">Bu öğretici, Hdınsight'ta oluşturma (Linux) Spark kümesinde Jupyter not defteri olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f7998-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="f7998-107">Not Defteri deneyimi Python parçacıkları dizüstü çalıştırmadan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7998-107">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="f7998-108">Gelen öğretici bir not defteri içinde gerçekleştirmek için bir Spark kümesi oluşturma, Jupyter not defteri başlatın (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), ve ardından not defteri çalıştırın **ile özel bir library.ipynb kullanarak Spark günlüklerini çözümleme** altında **PySpark**  klasörü.</span><span class="sxs-lookup"><span data-stu-id="f7998-108">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Analyze logs with Spark using a custom library.ipynb** under the **PySpark** folder.</span></span>
>
>

<span data-ttu-id="f7998-109">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="f7998-109">**Prerequisites:**</span></span>

<span data-ttu-id="f7998-110">Aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7998-110">You must have the following:</span></span>

* <span data-ttu-id="f7998-111">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="f7998-111">An Azure subscription.</span></span> <span data-ttu-id="f7998-112">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f7998-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="f7998-113">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="f7998-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f7998-114">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f7998-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="f7998-115">Ham veri bir RDD Kaydet</span><span class="sxs-lookup"><span data-stu-id="f7998-115">Save raw data as an RDD</span></span>
<span data-ttu-id="f7998-116">Bu bölümde, kullanırız [Jupyter](https://jupyter.org) ham örnek verileri işlemek ve Hive tablo olarak Kaydet işlerini çalıştırmak için hdınsight'ta bir Apache Spark kümesi ile ilişkili dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="f7998-116">In this section, we use the [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight to run jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="f7998-117">Örnek, bir .csv dosyası (hvac.csv) kullanılabilir varsayılan olarak tüm kümelerde verilerdir.</span><span class="sxs-lookup"><span data-stu-id="f7998-117">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="f7998-118">Verilerinizi bir Hive tablosu olarak kaydedildikten sonra sonraki bölümde biz Power BI ve Tableau gibi BI araçları kullanarak Hive tablosu bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f7998-118">Once your data is saved as a Hive table, in the next section we will connect to the Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="f7998-119">[Azure portalındaki](https://portal.azure.com/) başlangıç panosunda Spark kümenizin kutucuğuna tıklayın (başlangıç panosuna sabitlediyseniz).</span><span class="sxs-lookup"><span data-stu-id="f7998-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="f7998-120">Ayrıca **Browse All (Tümüne Gözat)** > **HDInsight Clusters (HDInsight Kümeleri)** altından kümenize gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7998-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="f7998-121">Spark kümesi dikey penceresinden **Küme Panosu**’na ve ardından **Jupyter Notebook**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f7998-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="f7998-122">İstenirse, küme için yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="f7998-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f7998-123">Aşağıdaki URL’yi tarayıcınızda açarak da Jupyter Notebook’a ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7998-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="f7998-124">**CLUSTERNAME** değerini kümenizin adıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="f7998-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="f7998-125">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f7998-125">Create a new notebook.</span></span> <span data-ttu-id="f7998-126">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f7998-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="f7998-127">![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Yeni bir Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="f7998-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="f7998-128">Yeni bir not defteri oluşturulur ve Untitled.pynb adı ile açılır.</span><span class="sxs-lookup"><span data-stu-id="f7998-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="f7998-129">Üstteki not defteri adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f7998-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="f7998-130">![Not defteri adını belirtme](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Not defteri adını belirtme")</span><span class="sxs-lookup"><span data-stu-id="f7998-130">![Provide a name for the notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for the notebook")</span></span>
5. <span data-ttu-id="f7998-131">PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için açıkça bir bağlam oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f7998-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="f7998-132">Birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f7998-132">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="f7998-133">Bu senaryo için gereken türleri içeri aktararak işleme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7998-133">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="f7998-134">Boş bir hücreye aşağıdaki kod parçacığını yapıştırın ve sonra basın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f7998-134">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="f7998-135">Kümede zaten mevcut örnek günlük verileri kullanarak bir RDD oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f7998-135">Create an RDD using the sample log data already available on the cluster.</span></span> <span data-ttu-id="f7998-136">Konumundaki küme ile ilişkili varsayılan depolama hesabındaki verilere erişebilir **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="f7998-136">You can access the data in the default storage account associated with the cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="f7998-137">Örnek günlük doğrulamak için kümesinin başarıyla tamamlandı ve önceki adımla alın.</span><span class="sxs-lookup"><span data-stu-id="f7998-137">Retrieve a sample log set to verify that the previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="f7998-138">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7998-138">You should see an output similar to the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="f7998-139">Özel bir Python kitaplığı kullanarak günlük verileri analiz</span><span class="sxs-lookup"><span data-stu-id="f7998-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="f7998-140">Yukarıdaki çıktıda üst bilgileri ilk birkaç satırı içerir ve bu başlığında açıklanan şema kalan her satırın eşleştirir.</span><span class="sxs-lookup"><span data-stu-id="f7998-140">In the output above, the first couple lines include the header information and each remaining line matches the schema described in that header.</span></span> <span data-ttu-id="f7998-141">Bu tür günlükleri ayrıştırma karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="f7998-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="f7998-142">Bu nedenle, özel bir Python kitaplığı kullandığımız (**iislogparser.py**) bu tür günlükleri çok daha kolay ayrıştırma yapar.</span><span class="sxs-lookup"><span data-stu-id="f7998-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="f7998-143">Varsayılan olarak, bu kitaplık hdınsight'ta Spark kümenizin birlikte **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="f7998-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="f7998-144">Ancak, bu kitaplık olmayan `PYTHONPATH` Biz bu gibi bir içeri aktarma deyimini kullanarak kullanamazlar `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="f7998-144">However, this library is not in the `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="f7998-145">Bu kitaplığı kullanmak için biz için tüm çalışan düğümleri dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7998-145">To use this library, we must distribute it to all the worker nodes.</span></span> <span data-ttu-id="f7998-146">Aşağıdaki kod parçacığında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f7998-146">Run the following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="f7998-147">`iislogparser`bir işlev sağlar `parse_log_line` döndüren `None` günlük satır bir başlık satırıdır ve örneğini döndürür, `LogLine` günlük satırı karşılaşırsa sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f7998-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of the `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="f7998-148">Kullanım `LogLine` sınıfı yalnızca günlük satırları RDD ayıklamak için:</span><span class="sxs-lookup"><span data-stu-id="f7998-148">Use the `LogLine` class to extract only the log lines from the RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="f7998-149">Birkaç doğrulamak için ayıklanan günlük satırları başarıyla tamamlandı adım alır.</span><span class="sxs-lookup"><span data-stu-id="f7998-149">Retrieve a couple of extracted log lines to verify that the step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="f7998-150">Çıktının aşağıdakine benzer olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7998-150">The output should be similar to the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="f7998-151">`LogLine` Sınıfı, sırasıyla sahip bazı kullanışlı yöntemler gibi `is_error()`, bir günlük girişi bir hata kodu sahip olup olmadığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="f7998-151">The `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="f7998-152">Ayıklanan günlük satırları hataların sayısı işlem için bunu kullanın ve farklı bir dosya için tüm hataların oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f7998-152">Use this to compute the number of errors in the extracted log lines, and then log all the errors to a different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="f7998-153">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7998-153">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="f7998-154">Aynı zamanda **Matplotlib** bir veri görselleştirmesi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f7998-154">You can also use **Matplotlib** to construct a visualization of the data.</span></span> <span data-ttu-id="f7998-155">Örneğin, uzun süredir çalışan istekleri nedenini ayırt etmek istiyorsanız, ortalama hizmet en zaman dosyaları bulmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7998-155">For example, if you want to isolate the cause of requests that run for a long time, you might want to find the files that take the most time to serve on average.</span></span>
   <span data-ttu-id="f7998-156">Aşağıdaki kod parçacığını bir isteğe hizmet vermek için çoğu sürdü üst 25 kaynakları alır.</span><span class="sxs-lookup"><span data-stu-id="f7998-156">The snippet below retrieves the top 25 resources that took most time to serve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="f7998-157">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7998-157">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="f7998-158">Ayrıca bu bilgileri çizim biçiminde sunabilir.</span><span class="sxs-lookup"><span data-stu-id="f7998-158">You can also present this information in the form of plot.</span></span> <span data-ttu-id="f7998-159">Bir çizim oluşturmak için ilk adım, bize ilk geçici bir tablo oluşturun **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="f7998-159">As a first step to create a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="f7998-160">Tablo günlükleri belirli bir zamanda herhangi bir olağan dışı gecikme ani olup olmadığını görmek için zamana göre gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="f7998-160">The table groups the logs by time to see if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="f7998-161">Ardından tüm kayıtları almak için aşağıdaki SQL sorgusunu çalıştırın **AverageTime** tablo.</span><span class="sxs-lookup"><span data-stu-id="f7998-161">You can then run the following SQL query to get all the records in the **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="f7998-162">`%%sql` Sihirli arkasından `-o averagetime` sorgu çıktısı (genellikle küme headnode) Jupyter sunucuda yerel olarak kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7998-162">The `%%sql` magic followed by `-o averagetime` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="f7998-163">Çıktı olarak kalıcı bir [Pandas](http://pandas.pydata.org/) belirtilen ada sahip dataframe **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="f7998-163">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **averagetime**.</span></span>

   <span data-ttu-id="f7998-164">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7998-164">You should see an output like the following:</span></span>

   <span data-ttu-id="f7998-165">![SQL sorgu çıktısı](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL sorgu çıktısı")</span><span class="sxs-lookup"><span data-stu-id="f7998-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="f7998-166">Hakkında daha fazla bilgi için `%%sql` Sihirli, bkz: [parametreleri desteklenen ile %% sql Sihirli](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="f7998-166">For more information about the `%%sql` magic, see [Parameters supported with the %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="f7998-167">Artık Matplotlib, veri görselleştirme oluşturmak için kullanılan bir kitaplık bir çizim oluşturmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7998-167">You can now use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="f7998-168">Çizim oluşturulması gerekir çünkü yerel olarak kalıcı gelen **averagetime** dataframe, kod parçacığında ile başlamalıdır `%%local` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="f7998-168">Because the plot must be created from the locally persisted **averagetime** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="f7998-169">Bu kodu Jupyter sunucu üzerinde yerel olarak çalıştırın sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7998-169">This ensures that the code is run locally on the Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="f7998-170">Aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7998-170">You should see an output like the following:</span></span>

   <span data-ttu-id="f7998-171">![Matplotlib çıkış](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib çıkış")</span><span class="sxs-lookup"><span data-stu-id="f7998-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="f7998-172">Uygulamayı çalıştırmayı tamamladıktan sonra kaynakları serbest bırakmak için not defterini kapatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7998-172">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="f7998-173">Bunu yapmak için not defterindeki **Dosya** menüsünde **Kapat ve Durdur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f7998-173">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="f7998-174">Bunun yapılması not defterini kapatır.</span><span class="sxs-lookup"><span data-stu-id="f7998-174">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="f7998-175"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f7998-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f7998-176">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="f7998-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f7998-177">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="f7998-177">Scenarios</span></span>
* [<span data-ttu-id="f7998-178">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="f7998-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f7998-179">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="f7998-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f7998-180">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="f7998-180">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f7998-181">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="f7998-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f7998-182">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f7998-182">Create and run applications</span></span>
* [<span data-ttu-id="f7998-183">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7998-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f7998-184">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f7998-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f7998-185">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="f7998-185">Tools and extensions</span></span>
* [<span data-ttu-id="f7998-186">Spark Scala uygulamaları oluşturmak ve göndermek amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisini kullanma</span><span class="sxs-lookup"><span data-stu-id="f7998-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f7998-187">Spark uygulamalarında uzaktan hata ayıklamak amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="f7998-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f7998-188">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="f7998-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f7998-189">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="f7998-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f7998-190">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="f7998-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f7998-191">Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="f7998-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f7998-192">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="f7998-192">Manage resources</span></span>
* [<span data-ttu-id="f7998-193">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="f7998-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f7998-194">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="f7998-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
