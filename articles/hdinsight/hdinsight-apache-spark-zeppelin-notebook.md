---
title: "Azure Hdınsight'ta Apache Spark aaaUse Zeppelin not defterlerini küme | Microsoft Docs"
description: "Azure Hdınsight'ta Apache Spark toouse Zeppelin not defterlerini kümeleri nasıl ilişkin adım adım yönergeler için."
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
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="40e86-103">Azure hdınsight'ta Apache Spark kümesinde ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="40e86-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="40e86-104">Hdınsight Spark kümeleri toorun Spark işlerinin kullanabileceğiniz Zeppelin not defterlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="40e86-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="40e86-105">Bu makalede, nasıl toouse hello Zeppelin Not Hdınsight kümesinde öğrenin.</span><span class="sxs-lookup"><span data-stu-id="40e86-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="40e86-106">Zeppelin not defterlerini yalnızca 1.6.3 Spark Hdınsight 3.5 ve 2.1.0 Spark Hdınsight 3.6 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="40e86-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="40e86-107">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="40e86-107">**Prerequisites:**</span></span>

* <span data-ttu-id="40e86-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="40e86-108">An Azure subscription.</span></span> <span data-ttu-id="40e86-109">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="40e86-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="40e86-110">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="40e86-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="40e86-111">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="40e86-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="40e86-112">Bir Zeppelin not defteri Başlat</span><span class="sxs-lookup"><span data-stu-id="40e86-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="40e86-113">Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Zeppelin not defteri**.</span><span class="sxs-lookup"><span data-stu-id="40e86-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="40e86-114">İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="40e86-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="40e86-115">Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Zeppelin Not Defteri de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="40e86-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="40e86-116">Değiştir **CLUSTERNAME** kümenizi hello adı:</span><span class="sxs-lookup"><span data-stu-id="40e86-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="40e86-117">Yeni bir not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40e86-117">Create a new notebook.</span></span> <span data-ttu-id="40e86-118">Merhaba üstbilgi Bölmesi'nden tıklatın **not defteri**ve ardından **oluşturma Yeni Not**.</span><span class="sxs-lookup"><span data-stu-id="40e86-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="40e86-119">![Yeni bir Zeppelin not defteri oluşturma](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "yeni bir Zeppelin not defteri oluşturma")</span><span class="sxs-lookup"><span data-stu-id="40e86-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="40e86-120">Merhaba dizüstü bilgisayar için bir ad girin ve ardından **oluşturma Not**.</span><span class="sxs-lookup"><span data-stu-id="40e86-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="40e86-121">Ayrıca, bağlı bir durum hello Not Defteri Başlığı gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="40e86-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="40e86-122">Merhaba sağ üst köşedeki yeşil bir nokta olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="40e86-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="40e86-123">![Zeppelin not defteri durumu](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin not defteri durumu")</span><span class="sxs-lookup"><span data-stu-id="40e86-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="40e86-124">Örnek verilerini geçici bir tabloya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="40e86-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="40e86-125">Merhaba örnek veri dosyası, Hdınsight'ta Spark kümesi oluşturduğunuzda, **hvac.csv**, kopyalanan toohello ilişkili depolama hesabı altında **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="40e86-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="40e86-126">Varsayılan olarak hello yeni not defterinde oluşturulan hello boş paragrafta, aşağıdaki kod parçacığında hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="40e86-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
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
   
    <span data-ttu-id="40e86-127">Tuşuna **SHIFT + ENTER** veya hello tıklatın **yürütmek** hello paragraf toorun hello parçacığı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="40e86-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="40e86-128">Merhaba paragrafın hello sağ köşesindeki Hello durumu hazır, BEKLİYOR, çalışan tooFINISHED gelen ilerleme.</span><span class="sxs-lookup"><span data-stu-id="40e86-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="40e86-129">Hello çıktısı görüntülenir hello hello altındaki aynı paragraf.</span><span class="sxs-lookup"><span data-stu-id="40e86-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="40e86-130">Merhaba ekran hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="40e86-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="40e86-131">![Ham verileri geçici bir tablo oluşturma](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "ham verilerden geçici bir tablo oluştur")</span><span class="sxs-lookup"><span data-stu-id="40e86-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="40e86-132">Başlık tooeach paragrafı sağlar.</span><span class="sxs-lookup"><span data-stu-id="40e86-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="40e86-133">Merhaba sağ köşesinden hello tıklatın **ayarları** simgesine ve ardından **Göster başlık**.</span><span class="sxs-lookup"><span data-stu-id="40e86-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="40e86-134">Artık hello üzerinde Spark SQL deyimlerini çalıştırabileceğiniz **hvac** tablo.</span><span class="sxs-lookup"><span data-stu-id="40e86-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="40e86-135">Yeni bir paragraf sorguda aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="40e86-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="40e86-136">Merhaba sorgu hello bina kimliği ve hello birbirinden hello hedef ve her belirli bir tarihte oluşturmaya yönelik gerçek etme alır.</span><span class="sxs-lookup"><span data-stu-id="40e86-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="40e86-137">Tuşuna **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="40e86-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="40e86-138">Merhaba **% sql** deyimi hello başında hello not defteri toouse hello Livy Scala yorumlayıcı söyler.</span><span class="sxs-lookup"><span data-stu-id="40e86-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="40e86-139">Merhaba aşağıdaki ekran görüntüsünde hello çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="40e86-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="40e86-140">![Merhaba Not Defteri kullanarak Spark SQL deyimini çalıştırın](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "hello Not Defteri kullanarak Spark SQL deyimini çalıştırın")</span><span class="sxs-lookup"><span data-stu-id="40e86-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="40e86-141">Merhaba görüntüleme seçenekleri (vurgulanmış dikdörtgen) tooswitch hello için farklı sunumu arasında tıklatın aynı çıktı.</span><span class="sxs-lookup"><span data-stu-id="40e86-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="40e86-142">Tıklatın **ayarları** toochoose anahtarı ve değerleri hello çıktısında ne consitutes hello.</span><span class="sxs-lookup"><span data-stu-id="40e86-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="40e86-143">Merhaba ekran yakalama kullanımlar yukarıda **buildingID** hello anahtar ve hello ortalama olarak **temp_diff** hello değeri olarak.</span><span class="sxs-lookup"><span data-stu-id="40e86-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="40e86-144">Merhaba sorguda değişkenler kullanarak Spark SQL deyimlerini de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40e86-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="40e86-145">Merhaba sonraki kod parçacığında gösterildiği nasıl toodefine bir değişken **Temp**, hello olası değerler ile Merhaba sorgusunda ile tooquery istiyor.</span><span class="sxs-lookup"><span data-stu-id="40e86-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="40e86-146">Hello sorgu ilk kez çalıştırdığınızda, bir açılan hello değişkeni için belirtilen hello değerlerle otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="40e86-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="40e86-147">Yeni bir paragraf ve tuşuna bu parçacığını yapıştırın **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="40e86-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="40e86-148">Merhaba aşağıdaki ekran görüntüsünde hello çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="40e86-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="40e86-149">![Merhaba Not Defteri kullanarak Spark SQL deyimini çalıştırın](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "hello Not Defteri kullanarak Spark SQL deyimini çalıştırın")</span><span class="sxs-lookup"><span data-stu-id="40e86-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="40e86-150">Sonraki sorgular için yeni bir değer hello açılan listeden seçin ve hello sorguyu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="40e86-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="40e86-151">Tıklatın **ayarları** toochoose anahtarı ve değerleri hello çıktısında ne consitutes hello.</span><span class="sxs-lookup"><span data-stu-id="40e86-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="40e86-152">Merhaba ekran yakalama kullanımlar yukarıda **buildingID** başlangıç anahtarı olarak ortalama hello **temp_diff** hello değeri olarak ve **targettemp** hello grubu olarak.</span><span class="sxs-lookup"><span data-stu-id="40e86-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="40e86-153">Merhaba Livy yorumlayıcı tooexit hello uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="40e86-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="40e86-154">toodo, bu nedenle, kullanıcı adı hello sağ üst köşesinden oturum hello tıklayarak yorumlayıcı ayarlarını açın ve ardından **yorumlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="40e86-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="40e86-155">![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")</span><span class="sxs-lookup"><span data-stu-id="40e86-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="40e86-156">TooLivy yorumlayıcı Ayarları'e gidin ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="40e86-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="40e86-157">![Merhaba Livy intepreter yeniden](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello Zeppelin intepreter yeniden başlatın")</span><span class="sxs-lookup"><span data-stu-id="40e86-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="40e86-158">Dış paketler hello not defteri ile nasıl kullanabilirim?</span><span class="sxs-lookup"><span data-stu-id="40e86-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="40e86-159">Merhaba Zeppelin not defteri dahil out-of--box hello kümede olmayan Hdınsight (Linux) toouse dış, topluluk katkıda bulunan paketler Apache Spark kümesinde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40e86-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="40e86-160">Merhaba arayabilirsiniz [Maven depo](http://search.maven.org/) hello tam kullanılabilir paketler listesi.</span><span class="sxs-lookup"><span data-stu-id="40e86-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="40e86-161">Ayrıca, diğer kaynaklardan kullanılabilir paketlerin listesini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40e86-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="40e86-162">Örneğin, tamamını topluluk katkıda bulunan paketlerin listesini adresten edinilebilir [Spark paketleri](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="40e86-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="40e86-163">Bu makalede, göreceğiniz nasıl toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) hello Jupyter not defteri paketiyle.</span><span class="sxs-lookup"><span data-stu-id="40e86-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="40e86-164">Yorumlayıcı Ayarları'nı açın.</span><span class="sxs-lookup"><span data-stu-id="40e86-164">Open interpreter settings.</span></span> <span data-ttu-id="40e86-165">Merhaba sağ üst köşesinden kullanıcı adı oturum hello tıklayın ve ardından **yorumlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="40e86-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="40e86-166">![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")</span><span class="sxs-lookup"><span data-stu-id="40e86-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="40e86-167">TooLivy yorumlayıcı Ayarları'e gidin ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="40e86-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="40e86-168">![Yorumlayıcı ayarları değiştirme](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "yorumlayıcı ayarlarını değiştir")</span><span class="sxs-lookup"><span data-stu-id="40e86-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="40e86-169">Yeni bir anahtar ekleyin adlı **livy.spark.jars.packages** ve hello biçiminde değerini ayarlama `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="40e86-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="40e86-170">Bunu, toouse hello istiyorsanız [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paketi değerine ayarlamanız gerekir hello hello anahtarının çok`com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="40e86-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="40e86-171">![Yorumlayıcı ayarları değiştirme](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "yorumlayıcı ayarlarını değiştir")</span><span class="sxs-lookup"><span data-stu-id="40e86-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="40e86-172">Tıklatın **kaydetmek** ve hello Livy yorumlayıcı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="40e86-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="40e86-173">**İpucu**: toounderstand nasıl tooarrive hello anahtarının hello değerde girilen burada yukarıdaki 's isteyip istemediğinizi nasıl.</span><span class="sxs-lookup"><span data-stu-id="40e86-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="40e86-174">a.</span><span class="sxs-lookup"><span data-stu-id="40e86-174">a.</span></span> <span data-ttu-id="40e86-175">Merhaba paketi hello Maven depo bulun.</span><span class="sxs-lookup"><span data-stu-id="40e86-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="40e86-176">Bu öğretici için kullandık [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="40e86-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="40e86-177">b.</span><span class="sxs-lookup"><span data-stu-id="40e86-177">b.</span></span> <span data-ttu-id="40e86-178">Merhaba depodan hello değerlerini toplamak **GroupID**, **Artifactıd**, ve **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="40e86-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="40e86-179">![Jupyter not defteri ile dış paketleri kullanma](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Jupyter not defteri ile dış paketleri kullanma")</span><span class="sxs-lookup"><span data-stu-id="40e86-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="40e86-180">c.</span><span class="sxs-lookup"><span data-stu-id="40e86-180">c.</span></span> <span data-ttu-id="40e86-181">Merhaba üç değerleri, virgülle ayrılmış birleştirme (**:**).</span><span class="sxs-lookup"><span data-stu-id="40e86-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="40e86-182">Merhaba kaydedilmiş Zeppelin not defterlerini nerede?</span><span class="sxs-lookup"><span data-stu-id="40e86-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="40e86-183">Merhaba Zeppelin not defterlerini toohello küme headnodes kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="40e86-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="40e86-184">Bu nedenle, hello kümeyi silmeniz halinde hello not defterlerini de silinir.</span><span class="sxs-lookup"><span data-stu-id="40e86-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="40e86-185">Toopreserve defterlerinizi diğer kümelerinde daha sonra kullanmak isterseniz, hello işleri çalıştırma bitirdikten sonra vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40e86-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="40e86-186">tooexport bir not defteri tıklatın hello **verme** hello resimde gösterildiği gibi simgesi.</span><span class="sxs-lookup"><span data-stu-id="40e86-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="40e86-187">![Not Defteri karşıdan](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "indirme hello not defteri")</span><span class="sxs-lookup"><span data-stu-id="40e86-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="40e86-188">Bu işlem hello dizüstü yükleme konumunuzu bir JSON dosyası olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="40e86-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="40e86-189">Livy oturum yönetimi</span><span class="sxs-lookup"><span data-stu-id="40e86-189">Livy session management</span></span>
<span data-ttu-id="40e86-190">Merhaba ilk kod paragraf Zeppelin not defterinde çalıştırdığınızda, yeni bir Livy oturum Hdınsight Spark kümenizin oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="40e86-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="40e86-191">Bu oturumda daha sonra oluşturduğunuz tüm Zeppelin not defterlerini arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="40e86-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="40e86-192">Bazı neden hello örneğin oturum Livy sonlandırıldı (küme yeniden başlatma, vb.), hello Zeppelin not defteri mümkün toorun işlerden olmaz.</span><span class="sxs-lookup"><span data-stu-id="40e86-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="40e86-193">Böyle bir durumda hello Zeppelin not defteri çalışan işler başlamadan önce aşağıdaki adımları gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40e86-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="40e86-194">Merhaba Livy yorumlayıcı hello Zeppelin not defteri gelen yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="40e86-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="40e86-195">toodo, bu nedenle, kullanıcı adı hello sağ üst köşesinden oturum hello tıklayarak yorumlayıcı ayarlarını açın ve ardından **yorumlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="40e86-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="40e86-196">![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")</span><span class="sxs-lookup"><span data-stu-id="40e86-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="40e86-197">TooLivy yorumlayıcı Ayarları'e gidin ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="40e86-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="40e86-198">![Merhaba Livy intepreter yeniden](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello Zeppelin intepreter yeniden başlatın")</span><span class="sxs-lookup"><span data-stu-id="40e86-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="40e86-199">Kod hücresini varolan bir Zeppelin not defterini ' çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="40e86-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="40e86-200">Bu yeni bir Livy oturum hello Hdınsight kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="40e86-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="40e86-201"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="40e86-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="40e86-202">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="40e86-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="40e86-203">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="40e86-203">Scenarios</span></span>
* [<span data-ttu-id="40e86-204">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="40e86-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="40e86-205">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="40e86-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="40e86-206">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="40e86-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="40e86-207">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="40e86-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="40e86-208">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="40e86-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="40e86-209">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="40e86-209">Create and run applications</span></span>
* [<span data-ttu-id="40e86-210">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="40e86-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="40e86-211">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="40e86-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="40e86-212">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="40e86-212">Tools and extensions</span></span>
* [<span data-ttu-id="40e86-213">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="40e86-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="40e86-214">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="40e86-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="40e86-215">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="40e86-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="40e86-216">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="40e86-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="40e86-217">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="40e86-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="40e86-218">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="40e86-218">Manage resources</span></span>
* [<span data-ttu-id="40e86-219">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="40e86-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="40e86-220">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="40e86-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







