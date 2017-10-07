---
title: "aaaSpark BI Azure Hdınsight'ta veri görselleştirme araçları kullanarak | Microsoft Docs"
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
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="3e46f-104">Apache Spark Azure Hdınsight ile verileri görselleştirme araçlarını kullanarak BI</span><span class="sxs-lookup"><span data-stu-id="3e46f-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="3e46f-105">Nasıl toouse veri görselleştirme gibi Power BI ve Tableau tooanalyze Hdınsight kümelerinde Apache Spark BI'ı kullanarak bir ham örnek veri kümesi araçları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-105">Learn how toouse data visualization tools such as Power BI and Tableau tooanalyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="3e46f-106">Bu makalede açıklanan BI araçları ile bağlantı Spark 2.1 Azure Hdınsight 3.6 Önizleme üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3e46f-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="3e46f-107">Yalnızca Spark sürüm 1.6 ve 2.0 (Hdınsight 3.4, 3.5 sırasıyla) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="3e46f-108">Bu öğretici, bir Hdınsight Spark kümesinde Jupyter not defteri olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="3e46f-109">Merhaba not defteri deneyimi hello Python parçacıkları hello dizüstü bilgisayarınızı kendisini çalıştırmadan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3e46f-109">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="3e46f-110">bir not defteri içinde tooperform hello öğretici bir Spark kümesi oluşturma, Jupyter not defteri başlatın (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), ve ardından hello dizüstü çalıştırın **HDInsight.ipynb Apache Spark kullanım BI araçlarıyla** hello altında **Python**  klasörü.</span><span class="sxs-lookup"><span data-stu-id="3e46f-110">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under hello **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e46f-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3e46f-111">Prerequisites</span></span>

* <span data-ttu-id="3e46f-112">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="3e46f-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="3e46f-113">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3e46f-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="3e46f-114"><a name="hivetable"></a>Spark veri görselleştirme için verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="3e46f-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="3e46f-115">Bu bölümde, hello kullanırız [Jupyter](https://jupyter.org) ham örnek verileri işlemek ve bir tablo olarak kaydetmek bir Hdınsight Spark küme toorun işleri dizüstü bilgisayarınızı.</span><span class="sxs-lookup"><span data-stu-id="3e46f-115">In this section, we use hello [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster toorun jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="3e46f-116">bir .csv dosyası (hvac.csv) kullanılabilir varsayılan olarak tüm kümelerde Hello örnek verilerdir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-116">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="3e46f-117">Verilerinizi bir tablo olarak kaydedildikten sonra sonraki bölümde hello biz BI araçları tooconnect toohello tabloyu kullanın ve veri görselleştirmeleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-117">Once your data is saved as a table, in hello next section we use BI tools tooconnect toohello table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="3e46f-118">Gerçekleştiriyorsanız hello bu makalede hello yönergeleri tamamladıktan sonra adımları [bir Hdınsight Spark kümesinde etkileşimli sorgular gerçekleştirme](hdinsight-apache-spark-load-data-run-query.md), tooStep 8 aşağıdaki atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e46f-118">If you are performing hello steps in this article after completing hello instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip tooStep 8 below.</span></span>
>

1. <span data-ttu-id="3e46f-119">Merhaba gelen [Azure portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="3e46f-120">Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="3e46f-121">Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="3e46f-122">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3e46f-123">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="3e46f-124">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="3e46f-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="3e46f-125">Bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e46f-125">Create a notebook.</span></span> <span data-ttu-id="3e46f-126">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="3e46f-127">![Apache Spark BI için bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "için Apache Spark BI Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="3e46f-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="3e46f-128">Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile.</span><span class="sxs-lookup"><span data-stu-id="3e46f-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="3e46f-129">Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="3e46f-130">![Apache Spark BI hello dizüstü bilgisayar için ad](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "için Apache Spark BI hello dizüstü bilgisayar için bir ad sağlayın")</span><span class="sxs-lookup"><span data-stu-id="3e46f-130">![Provide a name for hello notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for hello notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="3e46f-131">Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3e46f-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="3e46f-132">hello birinci kod hücresini çalıştırdığınızda hello Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3e46f-132">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="3e46f-133">Bu senaryo için gerekli hello türleri içeri aktararak işleme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e46f-133">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="3e46f-134">toodo hello hücre ve tuşuna hello imleç, yerleştirin **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-134">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="3e46f-135">Örnek verilerini geçici bir tabloya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="3e46f-136">Merhaba örnek veri dosyası, Hdınsight'ta Spark kümesi oluşturduğunuzda, **hvac.csv**, kopyalanan toohello ilişkili depolama hesabı altında **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-136">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="3e46f-137">Boş bir hücreye yapıştırın hello aşağıdaki kod parçacığında ve ENTER tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-137">In an empty cell, paste hello following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="3e46f-138">Bu kod parçacığında hello veri olarak adlandırılan bir tabloya kaydeder **hvac**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-138">This snippet registers hello data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. <span data-ttu-id="3e46f-139">Merhaba tablosunun başarıyla oluşturulduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e46f-139">Verify that hello table was successfully created.</span></span> <span data-ttu-id="3e46f-140">Merhaba kullanabilirsiniz `%%sql` toorun Hive sorguları doğrudan Sihirli.</span><span class="sxs-lookup"><span data-stu-id="3e46f-140">You can use hello `%%sql` magic toorun Hive queries directly.</span></span> <span data-ttu-id="3e46f-141">Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli ve hello PySpark çekirdeği kullanılabilen diğer sihirler bkz [Spark Hdınsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="3e46f-141">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="3e46f-142">Aşağıda gösterildiği gibi bir çıktı bakın:</span><span class="sxs-lookup"><span data-stu-id="3e46f-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="3e46f-143">Yalnızca false hello altında sahip tablolar hello **isTemporary** sütun olacak şekilde hello meta depo içinde saklanan ve hello BI Araçları'ndan erişilebilen hive tablosu.</span><span class="sxs-lookup"><span data-stu-id="3e46f-143">Only hello tables that have false under hello **isTemporary** column are hive tables that are stored in hello metastore and can be accessed from hello BI tools.</span></span> <span data-ttu-id="3e46f-144">Bu öğreticide, biz toohello bağlanmak **hvac** oluşturduğumuz tablo.</span><span class="sxs-lookup"><span data-stu-id="3e46f-144">In this tutorial, we connect toohello **hvac** table we created.</span></span>

8. <span data-ttu-id="3e46f-145">Merhaba tablosunun hello hedeflenen verileri içerdiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-145">Verify that hello table contains hello intended data.</span></span> <span data-ttu-id="3e46f-146">Boş bir hücreye hello Not, hello aşağıdakileri kopyalayın parçacığını ve tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-146">In an empty cell in hello notebook, copy hello following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="3e46f-147">Merhaba not defteri toorelease hello kaynakları kapatın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-147">Shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="3e46f-148">toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-148">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="3e46f-149"><a name="powerbi"></a>Power BI için Spark veri görselleştirme kullanın</span><span class="sxs-lookup"><span data-stu-id="3e46f-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="3e46f-150">Bu bölüm, yalnızca Hdınsight 3.4 üzerinde Spark 1.6 ve Hdınsight 3.5 Spark 2.0 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="3e46f-151">Merhaba verileri tablo olarak kaydettikten sonra Power BI tooconnect toohello verilerini kullanır ve toocreate raporları, görselleştirme vb. panoları.</span><span class="sxs-lookup"><span data-stu-id="3e46f-151">Once you have saved hello data as a table, you can use Power BI tooconnect toohello data and visualize it toocreate reports, dashboards, etc.</span></span>

1. <span data-ttu-id="3e46f-152">Erişim tooPower BI olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e46f-152">Make sure you have access tooPower BI.</span></span> <span data-ttu-id="3e46f-153">Power BI'dan, ücretsiz önizlemeye aboneliği alabilirsiniz [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="3e46f-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="3e46f-154">Çok oturum[Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="3e46f-154">Sign in too[Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="3e46f-155">Merhaba sol bölmesinde Hello aşağıdan tıklatın **Veri Al**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-155">From hello bottom of hello left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="3e46f-156">Merhaba üzerinde **Veri Al** sayfasında **alma veya tooData bağlanmak**, için **veritabanları**, tıklatın **almak**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-156">On hello **Get Data** page, under **Import or Connect tooData**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="3e46f-157">![Apache Spark BI için Power BI Veri Al](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "veri alma Power BI için Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="3e46f-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="3e46f-158">Merhaba sonraki ekranda, tıklatın **Azure hdınsight'ta Spark** ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-158">On hello next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="3e46f-159">İstendiğinde, hello kümesi URL'sini girin (`mysparkcluster.azurehdinsight.net`) ve hello kimlik bilgilerini tooconnect toohello küme.</span><span class="sxs-lookup"><span data-stu-id="3e46f-159">When prompted, enter hello cluster URL (`mysparkcluster.azurehdinsight.net`) and hello credentials tooconnect toohello cluster.</span></span>

    <span data-ttu-id="3e46f-160">![TooApache Spark BI bağlanmak](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "tooApache Spark BI Bağlan")</span><span class="sxs-lookup"><span data-stu-id="3e46f-160">![Connect tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect tooApache Spark BI")</span></span>

    <span data-ttu-id="3e46f-161">Merhaba bağlantı kurulduktan sonra Power BI hello Spark Hdınsight kümesinde veri alma başlatır.</span><span class="sxs-lookup"><span data-stu-id="3e46f-161">After hello connection is established, Power BI starts importing data from hello Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="3e46f-162">Power BI hello verileri alır ve ekler bir **Spark** dataset hello altında **veri kümeleri** başlığı.</span><span class="sxs-lookup"><span data-stu-id="3e46f-162">Power BI imports hello data and adds a **Spark** dataset under hello **Datasets** heading.</span></span> <span data-ttu-id="3e46f-163">Merhaba veri kümesi tooopen yeni çalışma sayfası toovisualize hello veri'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-163">Click hello data set tooopen a new worksheet toovisualize hello data.</span></span> <span data-ttu-id="3e46f-164">Bir rapor olarak hello çalışma da kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e46f-164">You can also save hello worksheet as a report.</span></span> <span data-ttu-id="3e46f-165">toosave bir çalışma hello sayfasından **dosya** menüsünde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-165">toosave a worksheet, from hello **File** menu, click **Save**.</span></span>

    <span data-ttu-id="3e46f-166">![Power BI panosundaki Apache Spark BI bölümünden](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI panosuna Apache Spark BI kutucuğu")</span><span class="sxs-lookup"><span data-stu-id="3e46f-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="3e46f-167">Bu hello fark **alanları** hello Sağdaki liste listeler hello **hvac** daha önce oluşturduğunuz tablo.</span><span class="sxs-lookup"><span data-stu-id="3e46f-167">Notice that hello **Fields** list on hello right lists hello **hvac** table you created earlier.</span></span> <span data-ttu-id="3e46f-168">Not defterinde daha önce tanımlanan hello tablo toosee hello alanları hello tablosundaki genişletin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-168">Expand hello table toosee hello fields in hello table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="3e46f-169">![Apache Spark BI Panoda Tabloları Listele](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Apache Spark BI Panoda Tabloları Listele")</span><span class="sxs-lookup"><span data-stu-id="3e46f-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="3e46f-170">Hedef sıcaklık ve her derleme için gerçek sıcaklık arasındaki görselleştirme tooshow hello fark oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e46f-170">Build a visualization tooshow hello variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="3e46f-171">toovisualize yoru verileri seçin **alan grafiği** (kırmızı kutu içinde gösterilmiştir).</span><span class="sxs-lookup"><span data-stu-id="3e46f-171">toovisualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="3e46f-172">toodefine hello eksen, sürükle ve bırak hello **BuildingID** altında **eksen**, ve **ActualTemp**/**TargetTemp** altında alanları **değeri**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-172">toodefine hello axis, drag-and-drop hello **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="3e46f-173">![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")</span><span class="sxs-lookup"><span data-stu-id="3e46f-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="3e46f-174">Varsayılan olarak hello görselleştirme için hello toplam gösterir **ActualTemp** ve **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-174">By default hello visualization shows hello sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="3e46f-175">Her ikisi de alanlardan hello aşağı açılan hello seçin **ortalama** tooget gerçek ortalama ve her iki binalar için hedef etme.</span><span class="sxs-lookup"><span data-stu-id="3e46f-175">For both hello fields, from hello drop-down, select **Average** tooget an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="3e46f-176">![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")</span><span class="sxs-lookup"><span data-stu-id="3e46f-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="3e46f-177">Veri görselleştirme benzer toohello bir hello ekran görüntüsü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-177">Your data visualization should be similar toohello one in hello screenshot.</span></span> <span data-ttu-id="3e46f-178">İmlecinizi hello görselleştirme tooget araç ipuçları ilgili verilerle üzerine getirin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-178">Move your cursor over hello visualization tooget tool tips with relevant data.</span></span>

    <span data-ttu-id="3e46f-179">![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")</span><span class="sxs-lookup"><span data-stu-id="3e46f-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="3e46f-180">Tıklatın **kaydetmek** hello gelen üst menüsünde ve bir rapor adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-180">Click **Save** from hello top menu and provide a report name.</span></span> <span data-ttu-id="3e46f-181">Merhaba visual de sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e46f-181">You can also pin hello visual.</span></span> <span data-ttu-id="3e46f-182">Bir görsel öğe PIN, böylece bir bakışta hello son değer izleyebilirsiniz Panonuzda depolanır.</span><span class="sxs-lookup"><span data-stu-id="3e46f-182">When you pin a visualization, it is stored on your dashboard so you can track hello latest value at a glance.</span></span>

   <span data-ttu-id="3e46f-183">İstediğiniz sayıda görsel öğeleri ekleyebilirsiniz hello aynı veri kümesi ve verilerinizin anlık görüntü için toohello Pano sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-183">You can add as many visualizations as you want for hello same dataset and pin them toohello dashboard for a snapshot of your data.</span></span> <span data-ttu-id="3e46f-184">Ayrıca, hdınsight'ta Spark kümeleri BI ile doğrudan bağlantı bağlı tooPower değildir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-184">Also, Spark clusters on HDInsight are connected tooPower BI with direct connect.</span></span> <span data-ttu-id="3e46f-185">Bu hello veri kümesi için tooschedule yenilemeleri gerek yoktur Power BI her zaman hello kümenizi en güncel verileri sahip olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3e46f-185">This ensures that Power BI always has hello most up-to-date data from your cluster so you do not need tooschedule refreshes for hello dataset.</span></span>

## <span data-ttu-id="3e46f-186"><a name="tableau"></a>Spark veri görselleştirme için Tableau Masaüstü'nü kullanın</span><span class="sxs-lookup"><span data-stu-id="3e46f-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="3e46f-187">Bu bölüm, yalnızca Azure Hdınsight'ta oluşturulan 1.5.2 Spark kümeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="3e46f-188">Yükleme [Tableau Masaüstü](http://www.tableau.com/products/desktop) bu Apache Spark BI öğretici çalıştırdığınız hello bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="3e46f-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on hello computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="3e46f-189">Bu bilgisayarda ayrıca Microsoft Spark ODBC sürücüsü yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e46f-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="3e46f-190">Merhaba sürücüsünden yükleyebilirsiniz [burada](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="3e46f-190">You can install hello driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="3e46f-191">Tableau Masaüstü başlatın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="3e46f-192">Merhaba sol bölmesinde, sunucu tooconnect için hello listesinden tıklatın **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-192">In hello left pane, from hello list of server tooconnect to, click **Spark SQL**.</span></span> <span data-ttu-id="3e46f-193">Spark SQL hello sol bölmesinde varsayılan olarak listelenmemişse tıklatın bulabilirsiniz **daha sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-193">If Spark SQL is not listed by default in hello left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="3e46f-194">Merhaba ekran görüntüsünde gösterildiği gibi Hello Spark SQL Bağlantısı iletişim kutusunda, hello değerler sağlayın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-194">In hello Spark SQL connection dialog box, provide hello values as shown in hello screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="3e46f-195">![Apache Spark BI için Bağlan tooa küme](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Bağlan tooa küme Apache Spark BI için")</span><span class="sxs-lookup"><span data-stu-id="3e46f-195">![Connect tooa cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect tooa cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="3e46f-196">kimlik doğrulama açılan listeleri hello **Microsoft Azure Hdınsight hizmeti** yalnızca hello yüklediyseniz bir seçenek olarak [Microsoft Spark ODBC sürücüsü](http://go.microsoft.com/fwlink/?LinkId=616229) hello bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="3e46f-196">hello authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed hello [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on hello computer.</span></span>
3. <span data-ttu-id="3e46f-197">Merhaba gelen hello sonraki ekranında **şema** açılan listesinde, hello tıklatın **Bul** simgesine ve ardından **varsayılan**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-197">On hello next screen, from hello **Schema** drop-down, click hello **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="3e46f-198">![Şema bulmak için Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Apache Spark BI Bul şeması")</span><span class="sxs-lookup"><span data-stu-id="3e46f-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="3e46f-199">Hello için **tablo** hello'ı tıklatın **Bul** simge tekrar tüm hello toolist Hive tabloları hello kümede kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3e46f-199">For hello **Table** field, click hello **Find** icon again toolist all hello Hive tables available in hello cluster.</span></span> <span data-ttu-id="3e46f-200">Merhaba görmelisiniz **hvac** önceki hello Not Defteri kullanarak oluşturduğunuz tablo.</span><span class="sxs-lookup"><span data-stu-id="3e46f-200">You should see hello **hvac** table you created earlier using hello notebook.</span></span>

    <span data-ttu-id="3e46f-201">![Tablo için Apache Spark BI Bul](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Apache Spark BI Bul tablosu")</span><span class="sxs-lookup"><span data-stu-id="3e46f-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="3e46f-202">Merhaba tablo toohello üst kutusunda sağ hello sürükleyip yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-202">Drag and drop hello table toohello top box on hello right.</span></span> <span data-ttu-id="3e46f-203">Tableau hello verileri alır ve hello şemasını hello kırmızı kutu ile vurgulanan görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3e46f-203">Tableau imports hello data and displays hello schema as highlighted by hello red box.</span></span>

    <span data-ttu-id="3e46f-204">![Tablolar tooTableau eklemek için Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "için Apache Spark BI tabloları tooTableau Ekle")</span><span class="sxs-lookup"><span data-stu-id="3e46f-204">![Add tables tooTableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables tooTableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="3e46f-205">Merhaba tıklatın **Sheet1** hello altındaki sol sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3e46f-205">Click hello **Sheet1** tab at hello bottom left.</span></span> <span data-ttu-id="3e46f-206">Merhaba ortalama hedef ve tüm binalar için gerçek etme her tarihini gösteren bir görsel öğe olun.</span><span class="sxs-lookup"><span data-stu-id="3e46f-206">Make a visualization that shows hello average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="3e46f-207">Sürükleme **tarih** ve **bina kimliği** çok**sütunları** ve **gerçek Temp**/**hedef Temp**çok**satırları**.</span><span class="sxs-lookup"><span data-stu-id="3e46f-207">Drag **Date** and **Building ID** too**Columns** and **Actual Temp**/**Target Temp** too**Rows**.</span></span> <span data-ttu-id="3e46f-208">Altında **işaretleri**seçin **alanı** toouse Spark veri görselleştirme için alan eşleme.</span><span class="sxs-lookup"><span data-stu-id="3e46f-208">Under **Marks**, select **Area** toouse an area map for Spark data visualization.</span></span>

     <span data-ttu-id="3e46f-209">![Spark veri görselleştirme için alanlar ekleyin](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Spark veri görselleştirme için alanlar ekleyin")</span><span class="sxs-lookup"><span data-stu-id="3e46f-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="3e46f-210">Varsayılan olarak, gösterilen hello sıcaklık alanlar toplama olarak.</span><span class="sxs-lookup"><span data-stu-id="3e46f-210">By default, hello temperature fields are shown as aggregate.</span></span> <span data-ttu-id="3e46f-211">Bunun yerine tooshow hello ortalama etme istiyorsanız hello açılan listeden, aşağıda gösterildiği gibi bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e46f-211">If you want tooshow hello average temperatures instead, you can do so from hello drop-down, as shown below.</span></span>

    <span data-ttu-id="3e46f-212">![Sıcaklık Spark veri görselleştirme için ortalama ele](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "sıcaklık Spark veri görselleştirme için ortalama alın")</span><span class="sxs-lookup"><span data-stu-id="3e46f-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="3e46f-213">Ayrıca Süper-bir ısı Haritası uygulayabilir üzerinde diğer tooget hedef gerçek etme arasındaki farkı daha iyi bir fikir hello.</span><span class="sxs-lookup"><span data-stu-id="3e46f-213">You can also super-impose one temperature map over hello other tooget a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="3e46f-214">Kırmızı bir daire vurgulanmış hello tanıtıcı şekli gördüğünüz kadar hello fare toohello köşe hello alt alan eşleme taşıyın.</span><span class="sxs-lookup"><span data-stu-id="3e46f-214">Move hello mouse toohello corner of hello lower area map till you see hello handle shape highlighted in a red circle.</span></span> <span data-ttu-id="3e46f-215">Kırmızı dikdörtgende vurgulanmış hello şekli gördüğünüzde hello harita toohello diğer harita üzerinde hello üst ve yayın hello fareyi sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-215">Drag hello map toohello other map on hello top and release hello mouse when you see hello shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="3e46f-216">![MAPS Spark veri görselleştirme için birleştirme](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "birleştirme eşler için Spark veri Görselleştirme")</span><span class="sxs-lookup"><span data-stu-id="3e46f-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="3e46f-217">Veri görselleştirme hello ekran görüntüsünde gösterildiği gibi değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3e46f-217">Your data visualization should change as shown in hello screenshot:</span></span>

    <span data-ttu-id="3e46f-218">![Spark veri görselleştirme için tableau çıkış](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau çıktı için Spark veri Görselleştirme")</span><span class="sxs-lookup"><span data-stu-id="3e46f-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="3e46f-219">Tıklatın **kaydetmek** toosave hello çalışma.</span><span class="sxs-lookup"><span data-stu-id="3e46f-219">Click **Save** toosave hello worksheet.</span></span> <span data-ttu-id="3e46f-220">Panolar oluşturun ve bir veya daha fazla sayfaları tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3e46f-220">You can create dashboards and add one or more sheets tooit.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e46f-221">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e46f-221">Next steps</span></span>

<span data-ttu-id="3e46f-222">Şu ana kadar toocreate bir küme Spark veri çerçeveleri tooquery verileri oluşturma ve ardından bu BI Araçları'ndan verilere öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="3e46f-222">So far you learned how toocreate a cluster, create Spark data frames tooquery data, and then access that data from BI tools.</span></span> <span data-ttu-id="3e46f-223">Şimdi nasıl toomanage küme kaynaklarını hello ve bir Hdınsight Spark kümesinde çalışan işlerin hata ayıklama yönergeleri bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e46f-223">You can now look at instructions on how toomanage hello cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="3e46f-224">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="3e46f-224">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3e46f-225">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="3e46f-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

