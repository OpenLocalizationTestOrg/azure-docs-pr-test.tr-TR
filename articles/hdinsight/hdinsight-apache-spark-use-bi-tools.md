---
title: "Spark Azure Hdınsight'ta veri görselleştirme araçları kullanarak BI | Microsoft Docs"
description: "Hdınsight kümelerinde Apache Spark BI'ı kullanarak analiz için verileri görselleştirme araçlarını kullanın"
keywords: "Apache spark BI, spark BI, spark veri görselleştirme, spark iş zekası"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 49dd161049ac442081fe6d26cf8bd3a56a2e0687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="81620-104">Apache Spark Azure Hdınsight ile verileri görselleştirme araçlarını kullanarak BI</span><span class="sxs-lookup"><span data-stu-id="81620-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="81620-105">Hdınsight kümelerinde Apache Spark BI'ı kullanarak bir ham örnek veri kümesi analiz etmek için Power BI ve Tableau gibi veri görselleştirme araçlarını kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="81620-105">Learn how to use data visualization tools such as Power BI and Tableau to analyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="81620-106">Bu makalede açıklanan BI araçları ile bağlantı Spark 2.1 Azure Hdınsight 3.6 Önizleme üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="81620-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="81620-107">Yalnızca Spark sürüm 1.6 ve 2.0 (Hdınsight 3.4, 3.5 sırasıyla) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="81620-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="81620-108">Bu öğretici, bir Hdınsight Spark kümesinde Jupyter not defteri olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="81620-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="81620-109">Not Defteri deneyimi Python parçacıkları dizüstü çalıştırmadan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="81620-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="81620-110">Gelen öğretici bir not defteri içinde gerçekleştirmek için bir Spark kümesi oluşturma, Jupyter not defteri başlatın (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), ve ardından not defteri çalıştırın **HDInsight.ipynb Apache Spark kullanım BI araçlarıyla** altında **Python** klasör.</span><span class="sxs-lookup"><span data-stu-id="81620-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81620-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="81620-111">Prerequisites</span></span>

* <span data-ttu-id="81620-112">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="81620-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="81620-113">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="81620-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="81620-114"><a name="hivetable"></a>Spark veri görselleştirme için verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="81620-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="81620-115">Bu bölümde, kullanırız [Jupyter](https://jupyter.org) ham örnek verileri işlemek ve bir tablo olarak kaydetmek işlerini çalıştırmak için Hdınsight Spark kümesinde dizüstü bilgisayarınızı.</span><span class="sxs-lookup"><span data-stu-id="81620-115">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="81620-116">Örnek, bir .csv dosyası (hvac.csv) kullanılabilir varsayılan olarak tüm kümelerde verilerdir.</span><span class="sxs-lookup"><span data-stu-id="81620-116">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="81620-117">Verilerinizi bir tablo olarak kaydedildikten sonra sonraki bölümde BI araçları tabloya bağlanmak ve veri görselleştirmeleri gerçekleştirmek için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="81620-117">Once your data is saved as a table, in the next section we use BI tools to connect to the table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="81620-118">Adımları bu makaledeki yönergeleri tamamladıktan sonra gerçekleştirdiğiniz varsa [bir Hdınsight Spark kümesinde etkileşimli sorgular gerçekleştirme](hdinsight-apache-spark-load-data-run-query.md), aşağıdaki adım 8'e atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-118">If you are performing the steps in this article after completing the instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip to Step 8 below.</span></span>
>

1. <span data-ttu-id="81620-119">[Azure portalındaki](https://portal.azure.com/) başlangıç panosunda Spark kümenizin kutucuğuna tıklayın (başlangıç panosuna sabitlediyseniz).</span><span class="sxs-lookup"><span data-stu-id="81620-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="81620-120">Ayrıca **Browse All (Tümüne Gözat)** > **HDInsight Clusters (HDInsight Kümeleri)** altından kümenize gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="81620-121">Spark kümesi dikey penceresinden **Küme Panosu**’na ve ardından **Jupyter Notebook**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81620-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="81620-122">İstenirse, küme için yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="81620-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="81620-123">Aşağıdaki URL’yi tarayıcınızda açarak da Jupyter Notebook’a ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="81620-124">**CLUSTERNAME** değerini kümenizin adıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="81620-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="81620-125">Bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81620-125">Create a notebook.</span></span> <span data-ttu-id="81620-126">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81620-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="81620-127">![Apache Spark BI için bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "için Apache Spark BI Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="81620-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="81620-128">Yeni bir not defteri oluşturulur ve Untitled.pynb adı ile açılır.</span><span class="sxs-lookup"><span data-stu-id="81620-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="81620-129">Üstteki not defteri adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="81620-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="81620-130">![Apache Spark BI için not defteri için ad](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "için Apache Spark BI dizüstü bilgisayar için bir ad sağlayın")</span><span class="sxs-lookup"><span data-stu-id="81620-130">![Provide a name for the notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for the notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="81620-131">PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için açıkça bir bağlam oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="81620-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="81620-132">Birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="81620-132">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="81620-133">Bu senaryo için gereken türleri içeri aktararak işleme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-133">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="81620-134">Bunu yapmak için imleci hücre ve tuşuna koyun **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="81620-134">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="81620-135">Örnek verilerini geçici bir tabloya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="81620-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="81620-136">HDInsight’ta bir Spark kümesi oluşturduğunuzda **hvac.csv** örnek veri dosyası, **\HdiSamples\HdiSamples\SensorSampleData\hvac** altındaki ilişkili depolama hesabına kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="81620-136">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="81620-137">Aşağıdaki kod parçacığında ve tuşuna boş bir hücreye yapıştırın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="81620-137">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="81620-138">Bu kod parçacığında veriler adı verilen bir tabloya kaydeder **hvac**.</span><span class="sxs-lookup"><span data-stu-id="81620-138">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="81620-139">Tablo başarıyla oluşturulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="81620-139">Verify that the table was successfully created.</span></span> <span data-ttu-id="81620-140">Kullanabileceğiniz `%%sql` Hive çalıştırmak için Sihirli sorgular doğrudan.</span><span class="sxs-lookup"><span data-stu-id="81620-140">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="81620-141">`%%sql` sihrinin yanı sıra PySpark çekirdeği kullanılabilen diğer sihirler hakkında daha fazla bilgi için bkz. [Spark HDInsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="81620-141">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="81620-142">Aşağıda gösterildiği gibi bir çıktı bakın:</span><span class="sxs-lookup"><span data-stu-id="81620-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="81620-143">False altında olan tabloları **isTemporary** sütun olacak şekilde meta depo içinde saklanan ve BI Araçları'ndan erişilebilen hive tablosu.</span><span class="sxs-lookup"><span data-stu-id="81620-143">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="81620-144">Bu öğreticide, biz bağlanmak **hvac** oluşturduğumuz tablo.</span><span class="sxs-lookup"><span data-stu-id="81620-144">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="81620-145">Tablo hedeflenen verileri içerdiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="81620-145">Verify that the table contains the intended data.</span></span> <span data-ttu-id="81620-146">Not defterindeki boş hücreye aşağıdaki kod parçacığında ve tuşuna kopyalama **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="81620-146">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="81620-147">Kaynakları serbest bırakmak için Not Defteri kapatın.</span><span class="sxs-lookup"><span data-stu-id="81620-147">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="81620-148">Bunu yapmak için not defterindeki **Dosya** menüsünde **Kapat ve Durdur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81620-148">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="81620-149"><a name="powerbi"></a>Power BI için Spark veri görselleştirme kullanın</span><span class="sxs-lookup"><span data-stu-id="81620-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="81620-150">Bu bölüm, yalnızca Hdınsight 3.4 üzerinde Spark 1.6 ve Hdınsight 3.5 Spark 2.0 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="81620-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="81620-151">Verileri tablo olarak kaydettikten sonra veri bağlanmak ve raporlar, panolar vb. oluşturmak üzere görselleştirmek için Power BI'ı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="81620-152">Power BI erişebildiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="81620-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="81620-153">Power BI'dan, ücretsiz önizlemeye aboneliği alabilirsiniz [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="81620-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="81620-154">Oturum [Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="81620-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="81620-155">Sol bölmede aşağıdan tıklatın **Veri Al**.</span><span class="sxs-lookup"><span data-stu-id="81620-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="81620-156">Üzerinde **Veri Al** sayfasında **alma veya verilere bağlanın**, için **veritabanları**, tıklatın **almak**.</span><span class="sxs-lookup"><span data-stu-id="81620-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="81620-157">![Apache Spark BI için Power BI Veri Al](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "veri alma Power BI için Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="81620-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="81620-158">Sonraki ekranda, tıklatın **Azure hdınsight'ta Spark** ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="81620-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="81620-159">İstendiğinde, kümesi URL'sini girin (`mysparkcluster.azurehdinsight.net`) ve kümeye bağlanmak için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="81620-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="81620-160">![Apache Spark BI bağlanmak](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Apache Spark BI Bağlan")</span><span class="sxs-lookup"><span data-stu-id="81620-160">![Connect to Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect to Apache Spark BI")</span></span>

    <span data-ttu-id="81620-161">Bağlantı kurulduktan sonra Power BI veri hdınsight'ta Spark kümesinde alma başlatır.</span><span class="sxs-lookup"><span data-stu-id="81620-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="81620-162">Power BI verileri alır ve ekler bir **Spark** veri kümesi altında **veri kümeleri** başlığı.</span><span class="sxs-lookup"><span data-stu-id="81620-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="81620-163">Verileri görselleştirmek için yeni bir çalışma sayfasını açmak için bu veri kümesi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="81620-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="81620-164">Bu gibi durumlarda, çalışma sayfası aynı zamanda bir rapor olarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="81620-165">Bir çalışma alanından kaydetmek için **dosya** menüsünde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="81620-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="81620-166">![Power BI panosundaki Apache Spark BI bölümünden](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI panosuna Apache Spark BI kutucuğu")</span><span class="sxs-lookup"><span data-stu-id="81620-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="81620-167">Dikkat **alanları** sağ listeleri listesinde **hvac** daha önce oluşturduğunuz tablo.</span><span class="sxs-lookup"><span data-stu-id="81620-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="81620-168">Not defterinde daha önce tanımlanan tablo alanları görmek için tabloyu genişletin.</span><span class="sxs-lookup"><span data-stu-id="81620-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="81620-169">![Apache Spark BI Panoda Tabloları Listele](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Apache Spark BI Panoda Tabloları Listele")</span><span class="sxs-lookup"><span data-stu-id="81620-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="81620-170">Hedef sıcaklık ve her derleme için gerçek sıcaklık arasındaki fark göstermek için bir görsel öğe oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81620-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="81620-171">Yoru verileri görselleştirmek için seçin **alan grafiği** (kırmızı kutu içinde gösterilmiştir).</span><span class="sxs-lookup"><span data-stu-id="81620-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="81620-172">Sürükle ve bırak ekseni tanımlamak için **BuildingID** altında **eksen**, ve **ActualTemp**/**TargetTemp** alanları altında **değeri**.</span><span class="sxs-lookup"><span data-stu-id="81620-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="81620-173">![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")</span><span class="sxs-lookup"><span data-stu-id="81620-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="81620-174">Varsayılan olarak görselleştirme için toplam gösterir **ActualTemp** ve **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="81620-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="81620-175">Her iki alanlardan, açılan seçin **ortalama** gerçek ortalama ve hedef etme için iki bina almak için.</span><span class="sxs-lookup"><span data-stu-id="81620-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="81620-176">![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")</span><span class="sxs-lookup"><span data-stu-id="81620-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="81620-177">Veri görselleştirme benzer ekran görüntüsü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="81620-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="81620-178">Araç ipuçları ile ilgili verileri almak için görselleştirme üzerinden imlecinizi taşıyın.</span><span class="sxs-lookup"><span data-stu-id="81620-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    <span data-ttu-id="81620-179">![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")</span><span class="sxs-lookup"><span data-stu-id="81620-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="81620-180">Tıklatın **kaydetmek** üstteki menüden ve bir rapor adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="81620-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="81620-181">Ayrıca visual sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-181">You can also pin the visual.</span></span> <span data-ttu-id="81620-182">Bir görsel öğe PIN, böylece bir bakışta son değer izleyebilirsiniz Panonuzda depolanır.</span><span class="sxs-lookup"><span data-stu-id="81620-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="81620-183">Aynı veri kümesi için istediğiniz ve bunları, verilerin bir anlık görüntüsünü panoya Sabitle sayıda görsel öğeleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="81620-184">Ayrıca, hdınsight'ta Spark kümeleri için Power BI ile doğrudan bağlı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="81620-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="81620-185">Bu veri kümesi için yenileme zamanlamanız gerekmez için Power BI her zaman en güncel verileri kümenizi sahip olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="81620-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <span data-ttu-id="81620-186"><a name="tableau"></a>Spark veri görselleştirme için Tableau Masaüstü'nü kullanın</span><span class="sxs-lookup"><span data-stu-id="81620-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="81620-187">Bu bölüm, yalnızca Azure Hdınsight'ta oluşturulan 1.5.2 Spark kümeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="81620-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="81620-188">Yükleme [Tableau Masaüstü](http://www.tableau.com/products/desktop) bu Apache Spark BI öğretici çalıştırdığınız bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="81620-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="81620-189">Bu bilgisayarda ayrıca Microsoft Spark ODBC sürücüsü yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="81620-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="81620-190">Sürücüsünden yükleyebilirsiniz [burada](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="81620-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="81620-191">Tableau Masaüstü başlatın.</span><span class="sxs-lookup"><span data-stu-id="81620-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="81620-192">Sol bölmede, bağlanmak üzere sunucu listesinden tıklatın **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="81620-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="81620-193">Sol bölmede varsayılan Spark SQL listelenmemişse tıklatın bulabilirsiniz **daha sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="81620-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="81620-194">Spark SQL Bağlantısı iletişim kutusunda aşağıdaki ekran görüntüsünde gösterildiği gibi değerler sağlayın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="81620-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="81620-195">![Apache Spark BI için bir kümeye Bağlan](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Apache Spark BI için bir kümeye Bağlan")</span><span class="sxs-lookup"><span data-stu-id="81620-195">![Connect to a cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="81620-196">Kimlik doğrulama açılan listeleri **Microsoft Azure Hdınsight hizmeti** yalnızca yüklediyseniz bir seçenek olarak [Microsoft Spark ODBC sürücüsü](http://go.microsoft.com/fwlink/?LinkId=616229) bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="81620-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="81620-197">Sonraki ekranda, gelen **şema** açılır menüsünde tıklatın **Bul** simgesine ve ardından **varsayılan**.</span><span class="sxs-lookup"><span data-stu-id="81620-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="81620-198">![Şema bulmak için Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Apache Spark BI Bul şeması")</span><span class="sxs-lookup"><span data-stu-id="81620-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="81620-199">İçin **tablo** alan, tıklatın **Bul** yeniden kümedeki kullanılabilir tüm Hive tablolarını listelemek için simge.</span><span class="sxs-lookup"><span data-stu-id="81620-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="81620-200">Görmeniz gerekir **hvac** daha önce Not Defteri kullanarak oluşturduğunuz tablo.</span><span class="sxs-lookup"><span data-stu-id="81620-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="81620-201">![Tablo için Apache Spark BI Bul](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Apache Spark BI Bul tablosu")</span><span class="sxs-lookup"><span data-stu-id="81620-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="81620-202">Sürükleyin ve üst kutusuna sağ taraftaki tablo bırakın.</span><span class="sxs-lookup"><span data-stu-id="81620-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="81620-203">Tableau verileri alır ve şema kırmızı kutu ile vurgulanan görüntüler.</span><span class="sxs-lookup"><span data-stu-id="81620-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="81620-204">![Ekleme tablolar için Tableau için Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "eklemek tablolar için Tableau için Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="81620-204">![Add tables to Tableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="81620-205">Tıklatın **Sheet1** sekmesi altındaki sol.</span><span class="sxs-lookup"><span data-stu-id="81620-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="81620-206">Tüm binalar için gerçek etme ve ortalama hedef her tarihini gösteren bir görsel öğe olun.</span><span class="sxs-lookup"><span data-stu-id="81620-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="81620-207">Sürükleme **tarih** ve **kimliği oluşturma** için **sütunları** ve **gerçek Temp**/**hedef Temp** için **satırları**.</span><span class="sxs-lookup"><span data-stu-id="81620-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="81620-208">Altında **işaretleri**seçin **alanı** bir alan eşlemesini Spark veri görselleştirme için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-208">Under **Marks**, select **Area** to use an area map for Spark data visualization.</span></span>

     <span data-ttu-id="81620-209">![Spark veri görselleştirme için alanlar ekleyin](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Spark veri görselleştirme için alanlar ekleyin")</span><span class="sxs-lookup"><span data-stu-id="81620-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="81620-210">Varsayılan olarak, gösterilen sıcaklık alanlar toplama olarak.</span><span class="sxs-lookup"><span data-stu-id="81620-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="81620-211">Bunun yerine ortalama etme göstermek istiyorsanız, açılan listeden, aşağıda gösterildiği gibi bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="81620-212">![Sıcaklık Spark veri görselleştirme için ortalama ele](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "sıcaklık Spark veri görselleştirme için ortalama alın")</span><span class="sxs-lookup"><span data-stu-id="81620-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="81620-213">Ayrıca Süper-bir ısı Haritası hedef gerçek etme arasındaki farkı daha iyi bir fikir almak için diğer üzerinden uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="81620-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="81620-214">Kırmızı bir daire vurgulanmış tanıtıcı şekli gördüğünüz kadar fareyi alt alan eşleme köşesine getirin.</span><span class="sxs-lookup"><span data-stu-id="81620-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="81620-215">Harita diğer eşlemeye üstte sürükleyin ve kırmızı dikdörtgende vurgulanan şekli gördüğünüzde fare düğmesini bırakın.</span><span class="sxs-lookup"><span data-stu-id="81620-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="81620-216">![MAPS Spark veri görselleştirme için birleştirme](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "birleştirme eşler için Spark veri Görselleştirme")</span><span class="sxs-lookup"><span data-stu-id="81620-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="81620-217">Veri görselleştirme ekran görüntüsünde gösterildiği gibi değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="81620-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="81620-218">![Spark veri görselleştirme için tableau çıkış](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau çıktı için Spark veri Görselleştirme")</span><span class="sxs-lookup"><span data-stu-id="81620-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="81620-219">Tıklatın **kaydetmek** çalışma kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="81620-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="81620-220">Panolar oluşturun ve bir veya daha fazla sayfa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="81620-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81620-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81620-221">Next steps</span></span>

<span data-ttu-id="81620-222">Şu ana kadar bir küme oluşturmak, veri çerçevelerini sorgu verileri için Spark oluşturun ve sonra BI Araçları'ndan bu verilere erişmek nasıl öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-222">So far you learned how to create a cluster, create Spark data frames to query data, and then access that data from BI tools.</span></span> <span data-ttu-id="81620-223">Şimdi, küme kaynaklarını yönetmek ve bir Hdınsight Spark kümesinde çalışan işlerin hata ayıklamak yönergeler da bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81620-223">You can now look at instructions on how to manage the cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="81620-224">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="81620-224">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="81620-225">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="81620-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

