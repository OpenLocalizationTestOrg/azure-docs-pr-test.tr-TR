---
title: "Azure Data Lake Store'da verileri çözümlemek için Apache Spark kullanın | Microsoft Docs"
description: "Azure Data Lake Store içinde depolanan verileri çözümlemek için Spark işleri çalıştırma"
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
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="88d27-103">Data Lake Store'da verileri çözümlemek üzere Hdınsight Spark kümesi kullanın</span><span class="sxs-lookup"><span data-stu-id="88d27-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="88d27-104">Bu öğreticide, Jupyter not defteri kullanılabilir Hdınsight Spark kümeleri ile bir Data Lake Store hesabından veri okuyan bir işi çalıştırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="88d27-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88d27-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="88d27-105">Prerequisites</span></span>

* <span data-ttu-id="88d27-106">Azure Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="88d27-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="88d27-107">[Azure Portal'ı kullanarak Azure Data Lake Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md) bölümündeki yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="88d27-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="88d27-108">Azure Hdınsight Spark, depolama alanı olarak Data Lake Store ile küme.</span><span class="sxs-lookup"><span data-stu-id="88d27-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="88d27-109">Bölümündeki yönergeleri izleyin [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="88d27-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="88d27-110">Verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="88d27-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="88d27-111">Varsayılan depolama olarak Data Lake Store ile Hdınsight küme oluşturduysanız bu adımı gerçekleştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="88d27-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="88d27-112">Küme oluşturma işlemlerini bazı örnek veri kümesi oluşturulurken belirtin Data Lake Store hesabındaki ekler.</span><span class="sxs-lookup"><span data-stu-id="88d27-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="88d27-113">Atla bölümüne [Data Lake Store ile kullanımı Hdınsight Spark kümesi](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="88d27-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="88d27-114">Ek depolama alanı ve varsayılan depolama alanı olarak Azure Storage Blobuna olarak Data Lake Store ile Hdınsight kümesi oluşturduysanız, Data Lake Store hesabına önce bazı örnek veriler üzerinde kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88d27-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="88d27-115">Azure depolama Blob verileri Hdınsight kümesi ile ilişkili örneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88d27-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="88d27-116">Kullanabileceğiniz [ADLCopy aracı](http://aka.ms/downloadadlcopy) Bunu yapmak için.</span><span class="sxs-lookup"><span data-stu-id="88d27-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="88d27-117">Karşıdan yükleme ve aracı bağlantıdan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="88d27-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="88d27-118">Bir komut istemi açın ve AdlCopy yüklü olduğu, genellikle dizinine gidin `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="88d27-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="88d27-119">Belirli bir blobu bir Data Lake Store'a kaynak kapsayıcıdan kopyalamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="88d27-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="88d27-120">Kopya **HVAC.csv** örnek veri dosyası konumunda **/HdiSamples/HdiSamples/SensorSampleData/hvac/** Azure Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="88d27-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="88d27-121">Kod parçacığı gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="88d27-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="88d27-122">Dosya ve yol adlarının doğru durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88d27-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="88d27-123">Data Lake Store hesabınızın altında elinizde Azure aboneliği için kimlik bilgilerini girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="88d27-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="88d27-124">Aşağıdakine benzer bir çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="88d27-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="88d27-125">Veri dosyası (**HVAC.csv**) altında bir klasöre kopyalanacak **/hvac** Data Lake Store hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="88d27-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="88d27-126">Hdınsight Spark kümesinde Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="88d27-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="88d27-127">[Azure Portal](https://portal.azure.com/)’daki başlangıç panosunda Spark kümenizin kutucuğuna tıklayın (başlangıç panosuna sabitlediyseniz).</span><span class="sxs-lookup"><span data-stu-id="88d27-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="88d27-128">Ayrıca **Tüm** > **HDInsight Kümelerine Gözat** altından kümenize gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88d27-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="88d27-129">Spark kümesi dikey penceresinden **Hızlı Bağlantılar**’a ve sonra **Küme Panosu** dikey penceresinden **Jupyter Not Defteri**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88d27-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="88d27-130">İstenirse, küme için yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="88d27-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="88d27-131">Aşağıdaki URL’yi tarayıcınızda açarak da Jupyter Notebook’a ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88d27-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="88d27-132">**CLUSTERNAME** değerini kümenizin adıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="88d27-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="88d27-133">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88d27-133">Create a new notebook.</span></span> <span data-ttu-id="88d27-134">**Yeni** ve ardından **PySpark** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88d27-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="88d27-135">![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Yeni bir Jupyter not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="88d27-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="88d27-136">PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için açıkça bir bağlam oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="88d27-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="88d27-137">Birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="88d27-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="88d27-138">Bu senaryo için gereken türleri içeri aktararak işleme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88d27-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="88d27-139">Bunu yapmak için aşağıdaki kod parçacığını bir hücreye yapıştırın ve **SHIFT + ENTER** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="88d27-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="88d27-140">Jupyter’de bir işi her çalıştırdığınızda web tarayıcınızın pencere başlığında not defteri başlığı ile birlikte **(Meşgul)** durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="88d27-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="88d27-141">Ayrıca sağ üst köşedeki **PySpark** metninin yanında içi dolu bir daire görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="88d27-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="88d27-142">İş tamamlandıktan sonra bu simge boş bir daireye dönüşür.</span><span class="sxs-lookup"><span data-stu-id="88d27-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="88d27-143">![Jupyter not defteri işinin durumu](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Jupyter not defteri işinin durumu")</span><span class="sxs-lookup"><span data-stu-id="88d27-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="88d27-144">Bir geçici tablo kullanarak örnek verileri yükleme **HVAC.csv** dosya Data Lake Store hesabına kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="88d27-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="88d27-145">Aşağıdaki URL deseni kullanarak Data Lake Store hesabındaki verilere erişebilir.</span><span class="sxs-lookup"><span data-stu-id="88d27-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="88d27-146">Data Lake Store varsayılan depolama varsa, HVAC.csv aşağıdaki URL'ye benzer yolundaki olacaktır:</span><span class="sxs-lookup"><span data-stu-id="88d27-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="88d27-147">Ya da aşağıdaki gibi kısaltılmış bir biçimi de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="88d27-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="88d27-148">Data Lake Store ek depolama alanı olarak varsa, HVAC.csv, gibi kopyaladığınız konumda olacaktır:</span><span class="sxs-lookup"><span data-stu-id="88d27-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="88d27-149">Aşağıdaki kod örneğinde boş bir hücreye yapıştırın, yerine **MYDATALAKESTORE** Data Lake Store hesap adı ve basın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="88d27-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="88d27-150">Bu kod örneği, verileri **hvac** adlı geçici bir tabloya kaydeder.</span><span class="sxs-lookup"><span data-stu-id="88d27-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="88d27-151">Bir PySpark çekirdeği kullandığınız için `%%sql` sihrini kullanarak yeni oluşturduğunuz **hvac** geçici tablosunda bundan böyle bir SQL sorgusunu doğrudan çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88d27-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="88d27-152">`%%sql` sihrinin yanı sıra PySpark çekirdeği kullanılabilen diğer sihirler hakkında daha fazla bilgi için bkz. [Spark HDInsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="88d27-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="88d27-153">İş başarıyla tamamlandıktan sonra varsayılan olarak aşağıdaki tablo çıktısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="88d27-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="88d27-154">![Sorgu sonucunun tablo çıktısı](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Sorgu sonucunun tablo çıktısı")</span><span class="sxs-lookup"><span data-stu-id="88d27-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="88d27-155">Sonuçları diğer görselleştirmelerde de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88d27-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="88d27-156">Örneğin, aynı çıktı için bir alan grafiği aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="88d27-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="88d27-157">![Sorgu sonucunun alan grafiği](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Sorgu sonucunun alan grafiği")</span><span class="sxs-lookup"><span data-stu-id="88d27-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="88d27-158">Uygulamayı çalıştırmayı tamamladıktan sonra kaynakları serbest bırakmak için not defterini kapatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88d27-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="88d27-159">Bunu yapmak için not defterindeki **Dosya** menüsünde **Kapat ve Durdur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88d27-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="88d27-160">Bunun yapılması not defterini kapatır.</span><span class="sxs-lookup"><span data-stu-id="88d27-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="88d27-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="88d27-161">Next steps</span></span>

* [<span data-ttu-id="88d27-162">Tek başına bir Apache Spark küme üzerinde çalışacak şekilde Scala uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="88d27-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="88d27-163">Hdınsight araçları Intellij için Azure Araç Seti Spark Hdınsight Spark Linux kümesi için uygulamalar oluşturmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="88d27-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="88d27-164">Hdınsight araçları Eclipse için Azure Araç Seti Spark Hdınsight Spark Linux kümesi için uygulamalar oluşturmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="88d27-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
