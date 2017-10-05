---
title: "Azure hdınsight'ta Apache Spark kümesinde ile Zeppelin not defterlerini kullanma | Microsoft Docs"
description: "Azure hdınsight'ta Apache Spark kümeleri ile Zeppelin not defterlerini kullanma hakkında adım adım yönergeler."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="350e5-103">Azure hdınsight'ta Apache Spark kümesinde ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="350e5-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="350e5-104">Hdınsight Spark kümeleri Spark işlerini çalıştırmak için kullanabileceğiniz Zeppelin not defterlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="350e5-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="350e5-105">Bu makalede bir Hdınsight kümesine Zeppelin not defteri kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="350e5-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="350e5-106">Zeppelin not defterlerini yalnızca 1.6.3 Spark Hdınsight 3.5 ve 2.1.0 Spark Hdınsight 3.6 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="350e5-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="350e5-107">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="350e5-107">**Prerequisites:**</span></span>

* <span data-ttu-id="350e5-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="350e5-108">An Azure subscription.</span></span> <span data-ttu-id="350e5-109">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="350e5-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="350e5-110">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="350e5-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="350e5-111">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="350e5-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="350e5-112">Bir Zeppelin not defteri Başlat</span><span class="sxs-lookup"><span data-stu-id="350e5-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="350e5-113">Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Zeppelin not defteri**.</span><span class="sxs-lookup"><span data-stu-id="350e5-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="350e5-114">İstenirse, küme için yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="350e5-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="350e5-115">Tarayıcınızda aşağıdaki URL'yi açarak kümeniz için Zeppelin Not Defteri de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="350e5-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="350e5-116">**CLUSTERNAME** değerini kümenizin adıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="350e5-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="350e5-117">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="350e5-117">Create a new notebook.</span></span> <span data-ttu-id="350e5-118">Üstbilgi Bölmesi'nden tıklatın **not defteri**ve ardından **oluşturma Yeni Not**.</span><span class="sxs-lookup"><span data-stu-id="350e5-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="350e5-119">![Yeni bir Zeppelin not defteri oluşturma](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "yeni bir Zeppelin not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="350e5-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="350e5-120">Dizüstü bilgisayar için bir ad girin ve ardından **oluşturma Not**.</span><span class="sxs-lookup"><span data-stu-id="350e5-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="350e5-121">Ayrıca, Not Defteri Başlığı bağlı durumu gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="350e5-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="350e5-122">Sağ üst köşedeki yeşil bir nokta olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="350e5-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="350e5-123">![Zeppelin not defteri durumu](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin not defteri durumu")</span><span class="sxs-lookup"><span data-stu-id="350e5-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="350e5-124">Örnek verilerini geçici bir tabloya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="350e5-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="350e5-125">Örnek veri dosyası olan Hdınsight'ta Spark kümesi oluşturduğunuzda **hvac.csv**, altındaki ilişkili depolama hesabına kopyalanır **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="350e5-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="350e5-126">Yeni not defterinde varsayılan olarak oluşturulan boş paragraf içinde aşağıdaki kod parçacığını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="350e5-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="350e5-127">Tuşuna **SHIFT + ENTER** veya tıklatın **yürütmek** kod parçacığında çalıştırmak paragraf düğmesi.</span><span class="sxs-lookup"><span data-stu-id="350e5-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="350e5-128">Paragraf sağ köşesindeki durumu, hazır BEKLEYEN, ÇALIŞTIĞINDAN tamamlandı kadar ilerleme.</span><span class="sxs-lookup"><span data-stu-id="350e5-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="350e5-129">Aynı paragraf alt kısmındaki çıkış gösterir.</span><span class="sxs-lookup"><span data-stu-id="350e5-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="350e5-130">Ekran aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="350e5-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="350e5-131">![Ham verileri geçici bir tablo oluşturma](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "ham verilerden geçici bir tablo oluştur")</span><span class="sxs-lookup"><span data-stu-id="350e5-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="350e5-132">Ayrıca, her paragraf başlık sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="350e5-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="350e5-133">Sağ köşesinden tıklatın **ayarları** simgesine ve ardından **Göster başlık**.</span><span class="sxs-lookup"><span data-stu-id="350e5-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="350e5-134">Üzerinde şimdi Spark SQL deyimlerini çalışabilir **hvac** tablo.</span><span class="sxs-lookup"><span data-stu-id="350e5-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="350e5-135">Aşağıdaki sorgu, yeni bir paragraf yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="350e5-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="350e5-136">Sorgu oluşturma kimliği ve her belirli bir tarihte oluşturmaya yönelik gerçek etme ve hedef arasındaki farkı alır.</span><span class="sxs-lookup"><span data-stu-id="350e5-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="350e5-137">Tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="350e5-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="350e5-138">**% Sql** başında deyimi Livy Scala yorumlayıcı kullanmak için Not Defteri söyler.</span><span class="sxs-lookup"><span data-stu-id="350e5-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="350e5-139">Aşağıdaki ekran görüntüsünde çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="350e5-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="350e5-140">![Not Defteri kullanarak Spark SQL deyimini çalıştırın](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Not Defteri kullanarak Spark SQL deyimini çalıştırın")</span><span class="sxs-lookup"><span data-stu-id="350e5-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="350e5-141">Aynı çıktı için farklı sunumu arasında geçiş yapmak için (dikdörtgende vurgulanan) görüntüleme seçeneklerini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="350e5-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="350e5-142">Tıklatın **ayarları** hangi consitutes çıktıda anahtarı ve değerleri seçin.</span><span class="sxs-lookup"><span data-stu-id="350e5-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="350e5-143">Yukarıdaki ekran yakalama kullanan **buildingID** anahtar ve ortalama olarak **temp_diff** değeri olarak.</span><span class="sxs-lookup"><span data-stu-id="350e5-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="350e5-144">Sorguda değişkenler kullanarak Spark SQL deyimlerini de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="350e5-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="350e5-145">Sonraki kod parçacığını bir değişkeni tanımlamak gösterilmiştir **Temp**, sorgudaki ile sorgulamak istediğiniz olası değerler ile.</span><span class="sxs-lookup"><span data-stu-id="350e5-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="350e5-146">Sorgu ilk kez çalıştırdığınızda, bir açılan değişken için belirtilen değerlerle otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="350e5-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="350e5-147">Yeni bir paragraf ve tuşuna bu parçacığını yapıştırın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="350e5-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="350e5-148">Aşağıdaki ekran görüntüsünde çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="350e5-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="350e5-149">![Not Defteri kullanarak Spark SQL deyimini çalıştırın](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Not Defteri kullanarak Spark SQL deyimini çalıştırın")</span><span class="sxs-lookup"><span data-stu-id="350e5-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="350e5-150">Sonraki sorgular için açılan listeden yeni bir değer seçin ve sorguyu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="350e5-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="350e5-151">Tıklatın **ayarları** hangi consitutes çıktıda anahtarı ve değerleri seçin.</span><span class="sxs-lookup"><span data-stu-id="350e5-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="350e5-152">Yukarıdaki ekran yakalama kullanan **buildingID** ortalamasını anahtar olarak **temp_diff** değeri olarak ve **targettemp** grup olarak.</span><span class="sxs-lookup"><span data-stu-id="350e5-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="350e5-153">Uygulamadan çıkmak için Livy yorumlayıcı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="350e5-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="350e5-154">Bunu yapmak için oturum açan kullanıcı adını sağ üst köşesinden tıklayarak yorumlayıcı Ayarları'nı açın ve ardından **yorumlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="350e5-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="350e5-155">![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")</span><span class="sxs-lookup"><span data-stu-id="350e5-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="350e5-156">Livy yorumlayıcı ayarlar'e gidin ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="350e5-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="350e5-157">![Livy intepreter yeniden](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Zeppelin intepreter yeniden başlatın")</span><span class="sxs-lookup"><span data-stu-id="350e5-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="350e5-158">Dış paketler not defteri ile nasıl kullanabilirim?</span><span class="sxs-lookup"><span data-stu-id="350e5-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="350e5-159">Dahil edilen out-of--box kümedeki olmayan dış, topluluk katkıda bulunan paketlerini kullanmak için Zeppelin Not Defteri (Linux) hdınsight'ta Apache Spark kümesinde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="350e5-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="350e5-160">Arama yapabilirsiniz [Maven depo](http://search.maven.org/) kullanılabilir paketler tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="350e5-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="350e5-161">Ayrıca, diğer kaynaklardan kullanılabilir paketlerin listesini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="350e5-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="350e5-162">Örneğin, tamamını topluluk katkıda bulunan paketlerin listesini adresten edinilebilir [Spark paketleri](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="350e5-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="350e5-163">Bu makalede, nasıl kullanılacağını görürsünüz [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) Jupyter not defteri paketiyle.</span><span class="sxs-lookup"><span data-stu-id="350e5-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="350e5-164">Yorumlayıcı Ayarları'nı açın.</span><span class="sxs-lookup"><span data-stu-id="350e5-164">Open interpreter settings.</span></span> <span data-ttu-id="350e5-165">Sağ üst köşesinden oturum açan kullanıcı adına tıklayın ve ardından **yorumlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="350e5-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="350e5-166">![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")</span><span class="sxs-lookup"><span data-stu-id="350e5-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="350e5-167">Livy yorumlayıcı ayarlar'e gidin ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="350e5-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="350e5-168">![Yorumlayıcı ayarları değiştirme](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "yorumlayıcı ayarlarını değiştir")</span><span class="sxs-lookup"><span data-stu-id="350e5-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="350e5-169">Yeni bir anahtar ekleyin adlı **livy.spark.jars.packages** ve biçiminde değerini ayarlama `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="350e5-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="350e5-170">Bunu kullanmak istiyorsanız, [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paketi, anahtar değerini ayarlamanız gerekir `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="350e5-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="350e5-171">![Yorumlayıcı ayarları değiştirme](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "yorumlayıcı ayarlarını değiştir")</span><span class="sxs-lookup"><span data-stu-id="350e5-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="350e5-172">Tıklatın **kaydetmek** ve Livy yorumlayıcı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="350e5-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="350e5-173">**İpucu**: adresindeki gelmesi öğrenmek istiyorsanız, anahtarın değerini Yukarıda girilen, burada nasıl.</span><span class="sxs-lookup"><span data-stu-id="350e5-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="350e5-174">a.</span><span class="sxs-lookup"><span data-stu-id="350e5-174">a.</span></span> <span data-ttu-id="350e5-175">Paket Maven deposunda bulun.</span><span class="sxs-lookup"><span data-stu-id="350e5-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="350e5-176">Bu öğretici için kullandık [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="350e5-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="350e5-177">b.</span><span class="sxs-lookup"><span data-stu-id="350e5-177">b.</span></span> <span data-ttu-id="350e5-178">Depodan değerlerini toplamak **GroupID**, **Artifactıd**, ve **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="350e5-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="350e5-179">![Jupyter not defteri ile dış paketleri kullanma](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Jupyter not defteri ile dış paketleri kullanma")</span><span class="sxs-lookup"><span data-stu-id="350e5-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="350e5-180">c.</span><span class="sxs-lookup"><span data-stu-id="350e5-180">c.</span></span> <span data-ttu-id="350e5-181">Virgülle ayrılmış üç değerden birleştirme (**:**).</span><span class="sxs-lookup"><span data-stu-id="350e5-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="350e5-182">Zeppelin not defterlerini kaydedildiği?</span><span class="sxs-lookup"><span data-stu-id="350e5-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="350e5-183">Zeppelin not defterlerini küme headnodes kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="350e5-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="350e5-184">Bu nedenle, kümeyi silmeniz halinde, dizüstü bilgisayarlar da silinir.</span><span class="sxs-lookup"><span data-stu-id="350e5-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="350e5-185">Diğer kümelerinde daha sonra kullanmak için not defterlerinizi korumak istiyorsanız, bir iş çalışmadığı bitirdikten sonra vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="350e5-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="350e5-186">Bir not defteri vermek için tıklatın **verme** aşağıdaki resimde gösterildiği gibi simgesi.</span><span class="sxs-lookup"><span data-stu-id="350e5-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="350e5-187">![Not Defteri karşıdan](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "not defteri indirin")</span><span class="sxs-lookup"><span data-stu-id="350e5-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="350e5-188">Bu, Not Defteri yükleme konumunuzu bir JSON dosyası olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="350e5-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="350e5-189">Livy oturum yönetimi</span><span class="sxs-lookup"><span data-stu-id="350e5-189">Livy session management</span></span>
<span data-ttu-id="350e5-190">İlk kod paragraf Zeppelin not defterinde çalıştırdığınızda, yeni bir Livy oturum Hdınsight Spark kümenizin oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="350e5-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="350e5-191">Bu oturumda daha sonra oluşturduğunuz tüm Zeppelin not defterlerini arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="350e5-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="350e5-192">(Küme yeniden başlatma, vb.) herhangi bir nedenden dolayı oturum Livy sonlandırıldı, işleri Zeppelin dizüstü bilgisayarınızı çalıştırabilir ve olmaz.</span><span class="sxs-lookup"><span data-stu-id="350e5-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="350e5-193">Böyle bir durumda, Zeppelin not defteri çalışan işler başlamadan önce aşağıdaki adımları gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="350e5-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="350e5-194">Livy yorumlayıcı Zeppelin not defteri gelen yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="350e5-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="350e5-195">Bunu yapmak için oturum açan kullanıcı adını sağ üst köşesinden tıklayarak yorumlayıcı Ayarları'nı açın ve ardından **yorumlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="350e5-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="350e5-196">![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")</span><span class="sxs-lookup"><span data-stu-id="350e5-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="350e5-197">Livy yorumlayıcı ayarlar'e gidin ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="350e5-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="350e5-198">![Livy intepreter yeniden](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Zeppelin intepreter yeniden başlatın")</span><span class="sxs-lookup"><span data-stu-id="350e5-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="350e5-199">Kod hücresini varolan bir Zeppelin not defterini ' çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="350e5-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="350e5-200">Bu, Hdınsight kümesinde yeni bir Livy oturum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="350e5-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="350e5-201"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="350e5-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="350e5-202">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="350e5-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="350e5-203">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="350e5-203">Scenarios</span></span>
* [<span data-ttu-id="350e5-204">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="350e5-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="350e5-205">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="350e5-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="350e5-206">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="350e5-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="350e5-207">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="350e5-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="350e5-208">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="350e5-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="350e5-209">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="350e5-209">Create and run applications</span></span>
* [<span data-ttu-id="350e5-210">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="350e5-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="350e5-211">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="350e5-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="350e5-212">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="350e5-212">Tools and extensions</span></span>
* [<span data-ttu-id="350e5-213">Spark Scala uygulamaları oluşturmak ve göndermek amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="350e5-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="350e5-214">Spark uygulamalarında uzaktan hata ayıklamak amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="350e5-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="350e5-215">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="350e5-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="350e5-216">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="350e5-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="350e5-217">Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="350e5-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="350e5-218">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="350e5-218">Manage resources</span></span>
* [<span data-ttu-id="350e5-219">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="350e5-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="350e5-220">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="350e5-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







