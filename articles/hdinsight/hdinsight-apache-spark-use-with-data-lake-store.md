---
title: Azure Data Lake Store'da Apache Spark tooanalyze veri aaaUse | Microsoft Docs
description: "Azure Data Lake Store'da depolanan tooanalyze verileri Spark işleri çalıştırma"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="0b6f1-103">Hdınsight Spark küme tooanalyze verileri Data Lake Store içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="0b6f1-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="0b6f1-104">Bu öğreticide, Hdınsight Spark kümeleri toorun bir Data Lake Store hesabından veri okuyan bir iş ile Jupyter not defteri kullanılabilir kullanın.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b6f1-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0b6f1-105">Prerequisites</span></span>

* <span data-ttu-id="0b6f1-106">Azure Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="0b6f1-107">Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0b6f1-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="0b6f1-108">Azure Hdınsight Spark, depolama alanı olarak Data Lake Store ile küme.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="0b6f1-109">Merhaba yönergeleri izleyin [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0b6f1-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="0b6f1-110">Merhaba verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="0b6f1-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="0b6f1-111">Varsayılan depolama olarak Data Lake Store ile Merhaba Hdınsight küme oluşturduysanız bu adımı tooperform gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="0b6f1-112">Merhaba küme oluşturma işlemlerini hello küme oluştururken belirttiğiniz hello Data Lake Store hesabındaki bazı örnek veri ekler.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="0b6f1-113">Atla toohello bölüm [Data Lake Store ile kullanımı Hdınsight Spark kümesi](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="0b6f1-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="0b6f1-114">Ek depolama alanı ve varsayılan depolama alanı olarak Azure Storage Blobuna olarak Data Lake Store ile Hdınsight kümesi oluşturduysanız, bazı örnek veri toohello Data Lake Store hesabı kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="0b6f1-115">Azure Storage Blobuna hello Hdınsight kümesi ile ilişkili hello hello örnek verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="0b6f1-116">Merhaba kullanabilirsiniz [ADLCopy aracı](http://aka.ms/downloadadlcopy) toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="0b6f1-117">Karşıdan yükle ve hello aracı hello bağlantıdan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="0b6f1-118">Bir komut istemi açın ve AdlCopy yüklü olduğu, genellikle toohello dizinine gidin `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="0b6f1-119">Komut toocopy aşağıdaki hello hello kaynak kapsayıcı tooa Data Lake Store belirli bir blobu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0b6f1-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="0b6f1-120">Kopya hello **HVAC.csv** örnek veri dosyası konumunda **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="0b6f1-121">Merhaba kod parçacığını gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="0b6f1-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="0b6f1-122">Dosya hello ve yol adları hello uygun durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="0b6f1-123">Merhaba kimlik bilgileri istendiğinde tooenter olacaktır Azure aboneliğinizin Data Lake Store hesabınızın altında elinizde hello.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="0b6f1-124">Bir çıkış benzer toohello aşağıdaki görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="0b6f1-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="0b6f1-125">Merhaba veri dosyası (**HVAC.csv**) altında bir klasöre kopyalanacak **/hvac** hello Data Lake Store hesabı içinde.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="0b6f1-126">Hdınsight Spark kümesinde Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="0b6f1-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="0b6f1-127">Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="0b6f1-128">Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="0b6f1-129">Merhaba Spark kümesi dikey penceresinden tıklatın **hızlı bağlantılar**ve sonra hello **küme Panosu** dikey penceresinde tıklatın **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="0b6f1-130">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0b6f1-131">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="0b6f1-132">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="0b6f1-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="0b6f1-133">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-133">Create a new notebook.</span></span> <span data-ttu-id="0b6f1-134">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="0b6f1-135">![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Yeni bir Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="0b6f1-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="0b6f1-136">Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="0b6f1-137">Merhaba birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları hello otomatik olarak sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="0b6f1-138">Bu senaryo için gerekli hello türleri içeri aktararak işleme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="0b6f1-139">toodo, bu nedenle, aşağıdaki kod parçacığını bir hücreye ve tuşuna hello yapıştırın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="0b6f1-140">Jupyter'de bir işi çalıştırma her zaman, web tarayıcınızın Pencere başlığında gösterecektir bir **(meşgul)** hello not defteri başlığı ile birlikte durum.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="0b6f1-141">Ayrıca bir daire sonraki toohello görürsünüz **PySpark** hello sağ üst köşedeki metin.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="0b6f1-142">Merhaba iş tamamlandıktan sonra bu tooa boş daire değiştirir.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="0b6f1-143">![Jupyter not defteri işinin durumu](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Jupyter not defteri işinin durumu")</span><span class="sxs-lookup"><span data-stu-id="0b6f1-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="0b6f1-144">Hello kullanarak geçici bir tabloya örnek verileri yükleme **HVAC.csv** toohello Data Lake Store hesabı kopyaladığınız dosya.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="0b6f1-145">URL deseni takip hello kullanarak hello Data Lake Store hesabındaki hello verilere erişebilir.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="0b6f1-146">Data Lake Store varsayılan depolama varsa, HVAC.csv URL aşağıdaki hello yolu benzer toohello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="0b6f1-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="0b6f1-147">Ya da kısaltılmış bir biçimi hello aşağıdaki gibi kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0b6f1-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="0b6f1-148">Data Lake Store ek depolama alanı olarak varsa, HVAC.csv, gibi kopyaladığınız hello konumda olacaktır:</span><span class="sxs-lookup"><span data-stu-id="0b6f1-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="0b6f1-149">Boş bir hücre, aşağıdaki kod örneğine Yapıştır hello yerine **MYDATALAKESTORE** Data Lake Store hesap adı ve basın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="0b6f1-150">Bu kod örneği hello veri adlı geçici bir tabloya kaydeder **hvac**.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="0b6f1-151">Bir PySpark çekirdeği kullandığınız için artık doğrudan bir SQL sorgusu hello geçici tablosunda çalıştırabilirsiniz **hvac** hello kullanarak yeni oluşturduğunuz `%%sql` Sihirli.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="0b6f1-152">Merhaba hakkında daha fazla bilgi için `%%sql` hello PySpark çekirdeği kullanılabilen diğer sihirler yanı sıra Sihirli bkz [Spark Hdınsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="0b6f1-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="0b6f1-153">Merhaba iş başarıyla tamamlandığında, tablo çıktısı aşağıdaki hello varsayılan olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="0b6f1-154">![Sorgu sonucunun tablo çıktısı](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Sorgu sonucunun tablo çıktısı")</span><span class="sxs-lookup"><span data-stu-id="0b6f1-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="0b6f1-155">Ayrıca hello sonuçları diğer görselleştirmelerde de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="0b6f1-156">Örneğin, bir alan grafiği için hello aynı çıktı hello şu şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="0b6f1-157">![Sorgu sonucunun alan grafiği](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Sorgu sonucunun alan grafiği")</span><span class="sxs-lookup"><span data-stu-id="0b6f1-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="0b6f1-158">Merhaba uygulaması çalıştıran bitirdikten sonra kapatma hello not defteri toorelease hello kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="0b6f1-159">toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="0b6f1-160">Bu işlem kapatma ve Kapat hello dizüstü.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0b6f1-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b6f1-161">Next steps</span></span>

* [<span data-ttu-id="0b6f1-162">Apache Spark kümesinde bir tek başına Scala uygulama toorun oluşturun</span><span class="sxs-lookup"><span data-stu-id="0b6f1-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0b6f1-163">Hdınsight araçları, Hdınsight Spark Linux kümesi için Intellij toocreate Spark uygulamaları için Azure araç setindeki kullanın.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0b6f1-164">Hdınsight araçları, Hdınsight Spark Linux kümesi için Eclipse toocreate Spark uygulamaları için Azure araç setindeki kullanın.</span><span class="sxs-lookup"><span data-stu-id="0b6f1-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
