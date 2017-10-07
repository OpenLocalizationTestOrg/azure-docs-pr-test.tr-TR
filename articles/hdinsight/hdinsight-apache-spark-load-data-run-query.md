---
title: "bir Azure Hdınsight Spark kümesinde aaaRun etkileşimli sorgular | Microsoft Docs"
description: "Hdınsight'ta bir Apache Spark toocreate küme nasıl üzerinde Hdınsight Spark hızlı başlangıç."
keywords: "spark hızlı başlangıç,etkileşimli spark,etkileşimli sorgu,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="a4038-104">Bir Hdınsight Spark kümesinde etkileşimli sorgular gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="a4038-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="a4038-105">Bu makalede, bir Jupyter not defteri toorun etkileşimli Spark SQL sorguları bir Spark kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4038-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="a4038-106">Jupyter not defteri hello konsol tabanlı etkileşimli deneyiminin toohello Web genişleten bir tarayıcı tabanlı bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="a4038-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="a4038-107">Daha fazla bilgi için bkz: [hello Jupyter not defteri](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="a4038-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="a4038-108">Bu öğretici için kullandığınız hello **PySpark** Çekirdeği'nde hello Jupyter not defteri toorun etkileşimli Spark SQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="a4038-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="a4038-109">Hdınsight kümeleri Jupyter not defterlerini destekleyen da iki diğer çekirdek - **PySpark3** ve **Spark**.</span><span class="sxs-lookup"><span data-stu-id="a4038-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="a4038-110">Hello tekrar ve hello kullanmanın avantajları hakkında daha fazla bilgi için **PySpark**, bkz: [Hdınsight'ta Apache Spark kullanım Jupyter not defterlerinde çekirdekler kümeleri](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="a4038-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4038-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a4038-111">Prerequisites</span></span>

* <span data-ttu-id="a4038-112">**Azure Hdınsight Spark kümesinde**.</span><span class="sxs-lookup"><span data-stu-id="a4038-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="a4038-113">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark kümesi oluşturma](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="a4038-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="a4038-114">Bir Jupyter not defteri toorun etkileşimli sorgular oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4038-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="a4038-115">toorun sorguları hello kümesi ile ilişkili hello depolama bulunan varsayılan örnek verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4038-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="a4038-116">Ancak, öncelikle bu veri Spark dataframe yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4038-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="a4038-117">Merhaba dataframe sahip olduğunda, sorguları hello Jupyter Not Defteri kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4038-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="a4038-118">Bu bölümde, nasıl bakın:</span><span class="sxs-lookup"><span data-stu-id="a4038-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="a4038-119">Bir örnek veri kümesi Spark dataframe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a4038-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="a4038-120">Sorgular hello dataframe üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="a4038-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="a4038-121">Açık hello [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a4038-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a4038-122">Toopin hello küme toohello Pano ettiyseniz, hello Pano toolaunch hello küme dikey penceresinden hello küme kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4038-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="a4038-123">Merhaba sol bölmesinden hello küme toohello Pano değil sabitlerseniz tıklatın **Hdınsight kümeleri**ve ardından oluşturduğunuz hello kümesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4038-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="a4038-124">**Hızlı bağlantılar** bölümünde **Küme panoları**'na ve ardından **Jupyter Notebook**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4038-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="a4038-125">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="a4038-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="a4038-126">![Açık Jupyter not defteri toorun etkileşimli Spark SQL sorgusu](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "açık Jupyter not defteri toorun etkileşimli Spark SQL sorgusu")</span><span class="sxs-lookup"><span data-stu-id="a4038-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="a4038-127">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4038-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="a4038-128">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="a4038-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="a4038-129">Bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4038-129">Create a notebook.</span></span> <span data-ttu-id="a4038-130">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4038-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="a4038-131">![Jupyter not defteri toorun etkileşimli Spark SQL sorgu oluşturma](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter not defteri toorun etkileşimli Spark SQL sorgu oluşturma")</span><span class="sxs-lookup"><span data-stu-id="a4038-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="a4038-132">Yeni bir not defteri oluşturulur ve Untitled(Untitled.pynb) hello adı ile açılır.</span><span class="sxs-lookup"><span data-stu-id="a4038-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="a4038-133">Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve isterseniz kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="a4038-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="a4038-134">![Merhaba Jupter not defteri toorun etkileşimli Spark sorgu için bir ad](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "hello Jupter not defteri toorun etkileşimli Spark sorgu için bir ad sağlayın")</span><span class="sxs-lookup"><span data-stu-id="a4038-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="a4038-135">Yapıştır hello aşağıdaki kod boş bir hücreye ve tuşuna basarak **SHIFT + ENTER** toorun hello kodu.</span><span class="sxs-lookup"><span data-stu-id="a4038-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="a4038-136">Merhaba kod bu senaryo için gerekli hello türleri alır:</span><span class="sxs-lookup"><span data-stu-id="a4038-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="a4038-137">Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a4038-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="a4038-138">hello birinci kod hücresini çalıştırdığınızda hello Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a4038-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="a4038-139">![Etkileşimli Spark SQL sorgusunun durumu](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span><span class="sxs-lookup"><span data-stu-id="a4038-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="a4038-140">Jupyter'de bir etkileşimli sorgusu her zaman, web tarayıcınızın Pencere başlığında gösteren bir **(meşgul)** hello not defteri başlığı ile birlikte durum.</span><span class="sxs-lookup"><span data-stu-id="a4038-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="a4038-141">Ayrıca dolu daire sonraki toohello bkz **PySpark** hello sağ üst köşedeki metin.</span><span class="sxs-lookup"><span data-stu-id="a4038-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="a4038-142">Merhaba iş tamamlandıktan sonra tooa boş daire değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a4038-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="a4038-143">Bir Spark küme içinde hello veri yükleme önce bize bir görüntüsünü bakın sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4038-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="a4038-144">Merhaba Bu öğreticide kullanılan örnek veriler tüm Hdınsight Spark kümeleri, bir CSV dosyası olarak kullanılabilir **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="a4038-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="a4038-145">Merhaba verileri bir yapı hello sıcaklık çeşitlemeleri yakalar.</span><span class="sxs-lookup"><span data-stu-id="a4038-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="a4038-146">Merhaba verilerin ilk birkaç satırı hello şunlardır.</span><span class="sxs-lookup"><span data-stu-id="a4038-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="a4038-147">![Etkileşimli Spark SQL sorgusu için verilerin anlık görüntüsünü](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "etkileşimli Spark SQL sorgusu için verilerin anlık görüntüsünü")</span><span class="sxs-lookup"><span data-stu-id="a4038-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="a4038-148">Bir dataframe ve geçici bir tablo oluşturma (**hvac**) koddan hello çalıştırarak.</span><span class="sxs-lookup"><span data-stu-id="a4038-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="a4038-149">Bu öğretici için size tüm hello sütunları hello geçici tabloya hello ham CSV verileri karşılaştırılan toohello sütun olarak oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="a4038-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="a4038-150">Merhaba verileri, etkileşimli sorgusu Hello tablo oluşturulduktan sonra aşağıdaki kodu hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4038-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="a4038-151">Bir PySpark çekirdeği kullandığınız için artık doğrudan etkileşimli bir SQL sorgusu hello geçici tablosunda çalıştırabilirsiniz **hvac** hello kullanılarak oluşturulan `%%sql` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="a4038-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="a4038-152">Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli ve hello PySpark çekirdeği kullanılabilen diğer sihirler bkz [Spark Hdınsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="a4038-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="a4038-153">Aşağıdaki tablo çıktısı hello varsayılan olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a4038-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="a4038-154">![Etkileşimli Spark sorgu sonucunun tablo çıktısı](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span><span class="sxs-lookup"><span data-stu-id="a4038-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="a4038-155">Ayrıca hello sonuçları diğer görselleştirmelerde de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4038-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="a4038-156">Örneğin, bir alan grafiği için hello aynı çıktı hello şu şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="a4038-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="a4038-157">![Etkileşimli Spark sorgu sonucunun alan grafiği](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span><span class="sxs-lookup"><span data-stu-id="a4038-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="a4038-158">Merhaba uygulaması çalıştıran bitirdikten sonra hello not defteri toorelease hello küme kaynaklarını kapatın.</span><span class="sxs-lookup"><span data-stu-id="a4038-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="a4038-159">toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.</span><span class="sxs-lookup"><span data-stu-id="a4038-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="a4038-160">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="a4038-160">Next step</span></span>

<span data-ttu-id="a4038-161">Bu, nasıl öğrenilen makale Jupyter Not Defteri kullanarak Spark toorun etkileşimli sorgular.</span><span class="sxs-lookup"><span data-stu-id="a4038-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="a4038-162">Power BI ve Tableau gibi BI analizi aracını içine nasıl Spark kayıtlı hello veri çekilen toohello sonraki makalede toosee ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="a4038-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="a4038-163">Spark Azure Hdınsight ile verileri görselleştirme araçlarını kullanarak BI</span><span class="sxs-lookup"><span data-stu-id="a4038-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




