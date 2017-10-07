---
title: "Spark - Azure Python kitaplıklarla aaaAnalyze Web sitesi günlüklerini | Microsoft Docs"
description: "Bu Not nasıl tooanalyze oturum Azure hdınsight'taki Spark ile özel bir kitaplık kullanılarak veri gösterir."
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
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="8addf-103">Hdınsight'ta Spark kümesinde ile özel bir Python kitaplığı kullanarak Web sitesi günlüklerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="8addf-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="8addf-104">Bu Not nasıl tooanalyze oturum hdınsight'ta Spark ile özel bir kitaplık kullanılarak veri gösterir.</span><span class="sxs-lookup"><span data-stu-id="8addf-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="8addf-105">kullanırız hello özel kitaplığıdır adlı bir Python Kitaplığı **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="8addf-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="8addf-106">Bu öğretici, Hdınsight'ta oluşturma (Linux) Spark kümesinde Jupyter not defteri olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8addf-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="8addf-107">Merhaba not defteri deneyimi hello Python parçacıkları hello dizüstü bilgisayarınızı kendisini çalıştırmadan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8addf-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="8addf-108">bir not defteri içinde tooperform hello öğretici bir Spark kümesi oluşturma, Jupyter not defteri başlatın (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), ve ardından hello dizüstü çalıştırın **ile özel bir library.ipynb kullanarak Spark günlüklerini çözümleme** hello altında  **PySpark** klasör.</span><span class="sxs-lookup"><span data-stu-id="8addf-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="8addf-109">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="8addf-109">**Prerequisites:**</span></span>

<span data-ttu-id="8addf-110">Merhaba şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8addf-110">You must have hello following:</span></span>

* <span data-ttu-id="8addf-111">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8addf-111">An Azure subscription.</span></span> <span data-ttu-id="8addf-112">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8addf-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="8addf-113">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="8addf-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8addf-114">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8addf-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="8addf-115">Ham veri bir RDD Kaydet</span><span class="sxs-lookup"><span data-stu-id="8addf-115">Save raw data as an RDD</span></span>
<span data-ttu-id="8addf-116">Bu bölümde, hello kullanırız [Jupyter](https://jupyter.org) ham örnek verileri işlemek ve Hive tablo olarak Kaydet Hdınsight toorun işleri Apache Spark kümesinde ile ilişkili dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="8addf-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="8addf-117">bir .csv dosyası (hvac.csv) kullanılabilir varsayılan olarak tüm kümelerde Hello örnek verilerdir.</span><span class="sxs-lookup"><span data-stu-id="8addf-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="8addf-118">Verilerinizi bir Hive tablosu olarak kaydedildikten sonra hello sonraki bölümde biz toohello Hive tablosu Power BI ve Tableau gibi BI araçları kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="8addf-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="8addf-119">Merhaba gelen [Azure portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8addf-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="8addf-120">Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="8addf-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="8addf-121">Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="8addf-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="8addf-122">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="8addf-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8addf-123">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="8addf-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="8addf-124">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="8addf-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="8addf-125">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8addf-125">Create a new notebook.</span></span> <span data-ttu-id="8addf-126">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8addf-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="8addf-127">![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Yeni bir Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="8addf-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="8addf-128">Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile.</span><span class="sxs-lookup"><span data-stu-id="8addf-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="8addf-129">Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8addf-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="8addf-130">![Merhaba dizüstü bilgisayar için bir ad](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "hello dizüstü bilgisayar için bir ad sağlayın")</span><span class="sxs-lookup"><span data-stu-id="8addf-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="8addf-131">Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8addf-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="8addf-132">Merhaba birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları hello otomatik olarak sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8addf-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="8addf-133">Bu senaryo için gerekli olan hello türleri içeri aktararak işleme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8addf-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="8addf-134">Boş bir hücre parçacığında aşağıdaki hello yapıştırın ve tuşuna basın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="8addf-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="8addf-135">Merhaba örnek günlük verilerini zaten kullanılabilir hello kümede kullanılarak RDD oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8addf-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="8addf-136">Merhaba kümesine ilişkili hello varsayılan depolama hesabı hello verilerine erişebilir **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="8addf-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="8addf-137">Önceki adımda başarıyla tamamlandı hello bir örnek günlük kümesi tooverify alın.</span><span class="sxs-lookup"><span data-stu-id="8addf-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="8addf-138">Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8addf-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="8addf-139">Özel bir Python kitaplığı kullanarak günlük verileri analiz</span><span class="sxs-lookup"><span data-stu-id="8addf-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="8addf-140">Merhaba çıkış yukarıdaki, o başlığında açıklanan hello şema her kalan satırıyla eşleşen ve hello ilk birkaç satırı hello üst bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="8addf-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="8addf-141">Bu tür günlükleri ayrıştırma karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="8addf-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="8addf-142">Bu nedenle, özel bir Python kitaplığı kullandığımız (**iislogparser.py**) bu tür günlükleri çok daha kolay ayrıştırma yapar.</span><span class="sxs-lookup"><span data-stu-id="8addf-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="8addf-143">Varsayılan olarak, bu kitaplık hdınsight'ta Spark kümenizin birlikte **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="8addf-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="8addf-144">Ancak, bu kitaplığı hello değil `PYTHONPATH` Biz bu gibi bir içeri aktarma deyimini kullanarak kullanamazlar `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="8addf-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="8addf-145">toouse bu kitaplığı biz tooall hello çalışan düğümleri dağıtmalısınız.</span><span class="sxs-lookup"><span data-stu-id="8addf-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="8addf-146">Aşağıdaki kod parçacığında hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8addf-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="8addf-147">`iislogparser`bir işlev sağlar `parse_log_line` döndüren `None` varsa bir günlük satırı sütun başlığı ve bir hello örneğini döndürür `LogLine` günlük satırı karşılaşırsa sınıfı.</span><span class="sxs-lookup"><span data-stu-id="8addf-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="8addf-148">Kullanım hello `LogLine` sınıfı tooextract yalnızca hello RDD günlük satırlarından hello:</span><span class="sxs-lookup"><span data-stu-id="8addf-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="8addf-149">Birkaç adım başarıyla tamamlandı hello ayıklanan günlük satırları tooverify alın.</span><span class="sxs-lookup"><span data-stu-id="8addf-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="8addf-150">Merhaba çıkış benzer toohello aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="8addf-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="8addf-151">Merhaba `LogLine` sınıfı, sırasıyla sahip bazı kullanışlı yöntemler gibi `is_error()`, bir günlük girişi bir hata kodu sahip olup olmadığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8addf-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="8addf-152">Bu toocompute hello hata sayısı ayıklanan hello günlük satırlarında kullanın ve ardından tüm hello hataları tooa farklı dosya oturum.</span><span class="sxs-lookup"><span data-stu-id="8addf-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="8addf-153">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8addf-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="8addf-154">Aynı zamanda **Matplotlib** tooconstruct hello veri görselleştirme.</span><span class="sxs-lookup"><span data-stu-id="8addf-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="8addf-155">Örneğin, uzun süredir çalışan istekleri tooisolate hello nedenini istiyorsanız hello çoğu zaman tooserve ortalama ele toofind hello dosyaları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8addf-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="8addf-156">Aşağıdaki Hello parçacığı çoğu zaman tooserve bir istek aldı hello üst 25 kaynakları alır.</span><span class="sxs-lookup"><span data-stu-id="8addf-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="8addf-157">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8addf-157">You should see an output like hello following:</span></span>

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
5. <span data-ttu-id="8addf-158">Ayrıca bu bilgileri çizimin hello formunda sunabilir.</span><span class="sxs-lookup"><span data-stu-id="8addf-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="8addf-159">Bir ilk adım toocreate bir çizim, bize ilk geçici bir tablo oluşturun **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="8addf-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="8addf-160">belirli bir zamanda herhangi bir olağan dışı gecikme ani olsaydı hello tablo grupları hello zaman toosee tarafından günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="8addf-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="8addf-161">Ardından SQL sorgu tooget aşağıdaki hello tüm hello kayıtları hello çalıştırabilirsiniz **AverageTime** tablo.</span><span class="sxs-lookup"><span data-stu-id="8addf-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="8addf-162">Merhaba `%%sql` Sihirli arkasından `-o averagetime` hello sorgu hello çıktısını (genellikle hello kümesinin hello headnode) hello Jupyter sunucuda yerel olarak kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8addf-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="8addf-163">Merhaba çıkış kalıcı olarak bir [Pandas](http://pandas.pydata.org/) dataframe hello ile belirtilen adı **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="8addf-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="8addf-164">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8addf-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="8addf-165">![SQL sorgu çıktısı](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL sorgu çıktısı")</span><span class="sxs-lookup"><span data-stu-id="8addf-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="8addf-166">Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli, bkz: [parametreleri ile Merhaba desteklenen %% sql Sihirli](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="8addf-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="8addf-167">Verilerin toocreate bir çizim tooconstruct görselleştirme kitaplığı kullanılan Matplotlib şimdi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8addf-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="8addf-168">Yerel olarak hello Hello çizim oluşturulması gerekir çünkü kalıcı **averagetime** dataframe, hello kod parçacığını hello ile başlamalıdır `%%local` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="8addf-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="8addf-169">Bu, hello kod hello Jupyter sunucusunda yerel olarak çalıştırın sağlar.</span><span class="sxs-lookup"><span data-stu-id="8addf-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="8addf-170">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8addf-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="8addf-171">![Matplotlib çıkış](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib çıkış")</span><span class="sxs-lookup"><span data-stu-id="8addf-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="8addf-172">Merhaba uygulaması çalıştıran bitirdikten sonra kapatma hello not defteri toorelease hello kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8addf-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="8addf-173">toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.</span><span class="sxs-lookup"><span data-stu-id="8addf-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="8addf-174">Bu işlem kapatma ve Kapat hello dizüstü.</span><span class="sxs-lookup"><span data-stu-id="8addf-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="8addf-175"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8addf-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8addf-176">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="8addf-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8addf-177">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="8addf-177">Scenarios</span></span>
* [<span data-ttu-id="8addf-178">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="8addf-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8addf-179">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8addf-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8addf-180">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="8addf-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8addf-181">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8addf-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8addf-182">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8addf-182">Create and run applications</span></span>
* [<span data-ttu-id="8addf-183">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="8addf-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8addf-184">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8addf-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8addf-185">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="8addf-185">Tools and extensions</span></span>
* [<span data-ttu-id="8addf-186">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="8addf-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8addf-187">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="8addf-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8addf-188">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="8addf-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8addf-189">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="8addf-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8addf-190">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="8addf-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="8addf-191">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="8addf-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8addf-192">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="8addf-192">Manage resources</span></span>
* [<span data-ttu-id="8addf-193">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8addf-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8addf-194">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="8addf-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
