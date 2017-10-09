---
title: "aaaDebug Apache Spark Azure Hdınsight üzerinde çalışan işleri | Microsoft Docs"
description: "Azure Hdınsight Spark kümesinde çalışan YARN kullanıcı Arabiriminde, Spark UI ve Spark geçmişi sunucu tootrack ve hata ayıklama işleri"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="66e91-103">Çalışan Azure Hdınsight'ta Apache Spark işleri hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="66e91-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="66e91-104">Bu makalede nasıl tootrack ve hata ayıklama hello YARN kullanıcı Arabiriminde, Spark UI kullanarak Hdınsight kümelerinde çalışan işleri Spark ve Spark geçmişi sunucu hello öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="66e91-105">Bu makalede, biz hello Spark kümesi ile kullanılabilir bir Not Defteri kullanarak Spark işi başlatacak **Machine learning: Yemek İnceleme verileri Mllib'i kullanarak Tahmine dayalı analiz**.</span><span class="sxs-lookup"><span data-stu-id="66e91-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="66e91-106">Örneğin, gönderilen tüm diğer yaklaşımı de kullanarak bir uygulama tootrack hello adımları kullanabilirsiniz **spark gönderme**.</span><span class="sxs-lookup"><span data-stu-id="66e91-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66e91-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="66e91-107">Prerequisites</span></span>
<span data-ttu-id="66e91-108">Merhaba şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="66e91-108">You must have hello following:</span></span>

* <span data-ttu-id="66e91-109">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="66e91-109">An Azure subscription.</span></span> <span data-ttu-id="66e91-110">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="66e91-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="66e91-111">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="66e91-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="66e91-112">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="66e91-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="66e91-113">Merhaba dizüstü çalıştıran başlamış olması gereken  **[Machine learning: Yemek İnceleme verileri Mllib'i kullanarak Tahmine dayalı analiz](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="66e91-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="66e91-114">Yönergeler için toorun bu not hello bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="66e91-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="66e91-115">Merhaba YARN kullanıcı Arabiriminde bir uygulamada izleme</span><span class="sxs-lookup"><span data-stu-id="66e91-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="66e91-116">Merhaba YARN kullanıcı Arabiriminde başlatın.</span><span class="sxs-lookup"><span data-stu-id="66e91-116">Launch hello YARN UI.</span></span> <span data-ttu-id="66e91-117">Merhaba küme dikey penceresinden tıklayın **küme Panosu**ve ardından **YARN**.</span><span class="sxs-lookup"><span data-stu-id="66e91-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![YARN kullanıcı arabirimini Başlat](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="66e91-119">Alternatif olarak, hello YARN kullanıcı Arabiriminde hello Ambari UI alanından başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="66e91-120">Merhaba küme dikey penceresinden toolaunch hello Ambari UI'ı tıklatın **küme Panosu**ve ardından **Hdınsight küme Panosu**.</span><span class="sxs-lookup"><span data-stu-id="66e91-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="66e91-121">Hello ifadesini Ambari UI'ı tıklatın **YARN**, tıklatın **hızlı bağlantılar**hello etkin Kaynak Yöneticisi'ni tıklatın ve ardından **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="66e91-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="66e91-122">Merhaba uygulaması hello ada sahip Jupyter not defterlerini kullanarak hello Spark iş başlatıldı olduğundan **remotesparkmagics** (Bu hello hello defterlerinden başlatılan tüm uygulamalar için addır).</span><span class="sxs-lookup"><span data-stu-id="66e91-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="66e91-123">Hello uygulama kimliği hello uygulama adı tooget karşı hello işi hakkında daha fazla bilgi'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66e91-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="66e91-124">Merhaba uygulama görünümünü başlatır.</span><span class="sxs-lookup"><span data-stu-id="66e91-124">This launches hello application view.</span></span>
   
    ![Spark uygulama kimliği bulunamıyor](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="66e91-126">Merhaba Jupyter defterlerinden başlatılan bu tür uygulamalar için hello durumu her zaman olan **çalıştıran** hello dizüstü çıkana kadar.</span><span class="sxs-lookup"><span data-stu-id="66e91-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="66e91-127">Merhaba uygulama görünümünden toofind hello uygulama ve hello günlükleri (stdout/stderr) ile ilişkili Merhaba kapsayıcılara çıkışı daha fazla ayrıntıya girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="66e91-128">Karşılık gelen toohello bağlama hello tıklayarak hello Spark UI başlatabilirsiniz **izleme URL'si**, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="66e91-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![Kapsayıcı günlüklerini indirin](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="66e91-130">Merhaba Spark UI uygulamada izleme</span><span class="sxs-lookup"><span data-stu-id="66e91-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="66e91-131">Hello Spark UI'da, daha önce başlatılmış hello uygulama tarafından kökenli hello Spark işlere ayrıntıya girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="66e91-132">Merhaba uygulama görünümünden toolaunch hello Spark UI hello karşı hello bağlantısını tıklatın **izleme URL'si**yukarıdaki hello ekran görüntüsünde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="66e91-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="66e91-133">Merhaba Jupyter not defteri çalışan hello uygulama tarafından başlatılan tüm hello Spark işleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Spark işleri görüntüle](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="66e91-135">Merhaba tıklatın **yürütücüler** sekmesinde toosee işleme ve depolama bilgi her Yürütücü için.</span><span class="sxs-lookup"><span data-stu-id="66e91-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="66e91-136">Merhaba üzerinde tıklayarak hello çağrı yığını alabilirsiniz **iş parçacığı dökümü** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="66e91-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Spark yürütücüler görüntüleyin](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="66e91-138">Merhaba tıklatın **aşamaları** sekmesinde toosee hello aşamaları hello uygulaması ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="66e91-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Görünüm Spark aşamaları](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="66e91-140">Her aşama için görüntüleyebilirsiniz yürütme istatistikleri, gibi birden çok görev sağlayabilirsiniz aşağıda gösterilen.</span><span class="sxs-lookup"><span data-stu-id="66e91-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Görünüm Spark aşamaları](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="66e91-142">Merhaba aşama Ayrıntılar sayfası, DAG görselleştirme başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="66e91-143">Merhaba genişletin **DAG görselleştirme** aşağıda gösterildiği gibi hello hello sayfanın başında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="66e91-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Görünüm Spark DAG görselleştirme aşamaları](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="66e91-145">DAG veya doğrudan Aclyic grafik Merhaba uygulaması farklı aşamalarda hello temsil eder.</span><span class="sxs-lookup"><span data-stu-id="66e91-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="66e91-146">Her hello grafik mavi kutuda hello uygulamadan çağrılan bir Spark işlemini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="66e91-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="66e91-147">Merhaba aşama Ayrıntılar sayfası, hello uygulama Zaman Çizelgesi görünümüne de başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="66e91-148">Merhaba genişletin **olay zaman çizelgesi** aşağıda gösterildiği gibi hello hello sayfanın başında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="66e91-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Olay Zaman Çizelgesi görünümüne Spark aşamaları](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="66e91-150">Bu, bir zaman çizelgesi hello biçiminde hello Spark olayları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="66e91-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="66e91-151">Merhaba Zaman Çizelgesi görünümüne üç düzeyde işleri, işindeki ve aşama içinde üzerinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="66e91-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="66e91-152">Yukarıdaki resimde Hello hello Zaman Çizelgesi görünümüne belirli bir aşama yakalar.</span><span class="sxs-lookup"><span data-stu-id="66e91-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="66e91-153">Merhaba seçerseniz **yakınlaştırma etkinleştirmek** onay kutusu kaydırma sol ve sağ hello zaman çizelgesi görünümü arasında.</span><span class="sxs-lookup"><span data-stu-id="66e91-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="66e91-154">Merhaba Spark UI diğer sekmeleri de hello Spark örneğinde hakkında yararlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="66e91-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="66e91-155">Uygulamanızı bir RDDs oluşturursa, depolama sekmesi - hello depolama sekmesi de hakkında bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="66e91-156">Ortam sekmesi - Bu sekme çok sayıda Spark örneğinizi hello gibi hakkında yararlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="66e91-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="66e91-157">Scala sürüm</span><span class="sxs-lookup"><span data-stu-id="66e91-157">Scala version</span></span>
     * <span data-ttu-id="66e91-158">Olay günlüğüne directory Hello kümesi ile ilişkili</span><span class="sxs-lookup"><span data-stu-id="66e91-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="66e91-159">Merhaba uygulaması için Yürütücü çekirdek sayısı</span><span class="sxs-lookup"><span data-stu-id="66e91-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="66e91-160">Etc.</span><span class="sxs-lookup"><span data-stu-id="66e91-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="66e91-161">Tamamlanan İşler hello Spark geçmişi sunucu kullanma hakkında bilgi</span><span class="sxs-lookup"><span data-stu-id="66e91-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="66e91-162">Bir iş tamamlandığında, hello işle ilgili hello bilgileri hello Spark geçmişi sunucu kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="66e91-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="66e91-163">Merhaba küme dikey penceresinden toolaunch hello Spark geçmişi sunucu tıklatın **küme Panosu**ve ardından **Spark geçmişi sunucu**.</span><span class="sxs-lookup"><span data-stu-id="66e91-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Spark geçmişi sunucu başlatma](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="66e91-165">Alternatif olarak, hello Spark geçmişi sunucu UI hello Ambari UI alanından başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e91-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="66e91-166">Merhaba küme dikey penceresinden toolaunch hello Ambari UI'ı tıklatın **küme Panosu**ve ardından **Hdınsight küme Panosu**.</span><span class="sxs-lookup"><span data-stu-id="66e91-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="66e91-167">Hello ifadesini Ambari UI'ı tıklatın **Spark**, tıklatın **hızlı bağlantılar**ve ardından **Spark geçmişi sunucu UI**.</span><span class="sxs-lookup"><span data-stu-id="66e91-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="66e91-168">Listelenen tüm tamamlanan hello uygulamaları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="66e91-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="66e91-169">Bir uygulama kimliği toodrill bir uygulamaya daha fazla bilgi için aşağıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66e91-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Spark geçmişi sunucu başlatma](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="66e91-171">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="66e91-171">See also</span></span>
*  [<span data-ttu-id="66e91-172">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="66e91-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="66e91-173">Veri çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="66e91-173">For data analysts</span></span>

* [<span data-ttu-id="66e91-174">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="66e91-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="66e91-175">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="66e91-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="66e91-176">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="66e91-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="66e91-177">HDInsight’ta Spark kullanarak Application Insight telemetri verilerinin analizi</span><span class="sxs-lookup"><span data-stu-id="66e91-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="66e91-178">Caffe Azure Hdınsight Spark üzerinde dağıtılmış derin learning için kullanın.</span><span class="sxs-lookup"><span data-stu-id="66e91-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="66e91-179">Spark geliştiricileri için</span><span class="sxs-lookup"><span data-stu-id="66e91-179">For Spark developers</span></span>

* [<span data-ttu-id="66e91-180">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="66e91-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="66e91-181">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="66e91-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="66e91-182">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="66e91-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="66e91-183">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="66e91-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="66e91-184">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="66e91-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="66e91-185">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="66e91-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="66e91-186">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="66e91-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="66e91-187">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="66e91-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="66e91-188">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="66e91-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


