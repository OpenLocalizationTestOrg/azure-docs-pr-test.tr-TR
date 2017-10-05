---
title: "Azure hdınsight'ta Apache Spark kümesi ile ilgili sorunları giderme | Microsoft Docs"
description: "Azure Hdınsight ve bunlar nasıl Apache Spark kümeleri ile ilgili sorunlar hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="8e71c-103">Hdınsight'ta Apache Spark kümesi için bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="8e71c-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="8e71c-104">Bu belge bilinen sorunlar Hdınsight Spark genel Önizleme için izler.</span><span class="sxs-lookup"><span data-stu-id="8e71c-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="8e71c-105">Etkileşimli oturum Livy sızdırıyor</span><span class="sxs-lookup"><span data-stu-id="8e71c-105">Livy leaks interactive session</span></span>
<span data-ttu-id="8e71c-106">Bir etkileşimli oturum hala canlı Livy (Ambari veya headnode 0 sanal makine yeniden başlatma nedeniyle) yeniden başlatıldığında bir etkileşimli iş oturumu sızmasını.</span><span class="sxs-lookup"><span data-stu-id="8e71c-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="8e71c-107">Bu nedenle, yeni işleri görüp kabul edilen durumda ve başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="8e71c-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="8e71c-108">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="8e71c-108">**Mitigation:**</span></span>

<span data-ttu-id="8e71c-109">Sorunun geçici çözümü için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="8e71c-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="8e71c-110">SSH headnode içine.</span><span class="sxs-lookup"><span data-stu-id="8e71c-110">Ssh into headnode.</span></span> <span data-ttu-id="8e71c-111">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8e71c-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8e71c-112">Livy başlatılan etkileşimli işleri uygulama kimliklerini bulmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8e71c-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="8e71c-113">Adları için Livy oturum Jupyter not defteri tarafından başlatılan işleri Livy etkileşimli oturum hiçbir açık adlarıyla ile başlatılmış Livy belirtilen olacaktır varsayılan iş iş adı remotesparkmagics_ * ile başlar.</span><span class="sxs-lookup"><span data-stu-id="8e71c-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="8e71c-114">Bu işleri sonlandırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8e71c-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="8e71c-115">Yeni iş çalışmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="8e71c-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="8e71c-116">Spark geçmişi sunucu başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="8e71c-116">Spark History Server not started</span></span>
<span data-ttu-id="8e71c-117">Spark geçmişi sunucu bir küme oluşturulduktan sonra otomatik olarak başlatılan bir dosya değil.</span><span class="sxs-lookup"><span data-stu-id="8e71c-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="8e71c-118">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="8e71c-118">**Mitigation:**</span></span> 

<span data-ttu-id="8e71c-119">El ile geçmişi sunucunun Ambari başlatın.</span><span class="sxs-lookup"><span data-stu-id="8e71c-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="8e71c-120">Spark günlük dizini izin sorunu</span><span class="sxs-lookup"><span data-stu-id="8e71c-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="8e71c-121">Hdiuser spark-submit işlemiyle gönderdiğinde, bir hata java.io.FileNotFoundException yoktur: /var/log/spark/sparkdriver_hdiuser.log (izni reddedildi) ve sürücü günlük yazılmadı.</span><span class="sxs-lookup"><span data-stu-id="8e71c-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="8e71c-122">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="8e71c-122">**Mitigation:**</span></span>

1. <span data-ttu-id="8e71c-123">Hdiuser Hadoop grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8e71c-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="8e71c-124">777 izinleri üzerinde /var/log/spark Küme oluşturulduktan sonra sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8e71c-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="8e71c-125">Bir dizin 777 izinlerine sahip olması için Ambari kullanarak spark günlük konumunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8e71c-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="8e71c-126">Çalışma spark-gönderme sudo.</span><span class="sxs-lookup"><span data-stu-id="8e71c-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="8e71c-127">Spark Phoenix bağlayıcı desteklenmez</span><span class="sxs-lookup"><span data-stu-id="8e71c-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="8e71c-128">Şu anda, Spark Phoenix bağlayıcı Hdınsight Spark kümesinde ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="8e71c-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="8e71c-129">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="8e71c-129">**Mitigation:**</span></span>

<span data-ttu-id="8e71c-130">Bunun yerine Spark HBase Bağlayıcısı'nı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e71c-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="8e71c-131">Yönergeler için bkz [Spark HBase bağlayıcıyı kullanmak üzere nasıl](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="8e71c-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="8e71c-132">Jupyter not defterleri için ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="8e71c-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="8e71c-133">Jupyter not defterleri için ilgili bazı bilinen sorunlar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8e71c-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="8e71c-134">Dizüstü bilgisayarlarla dosya adları ASCII olmayan karakterler</span><span class="sxs-lookup"><span data-stu-id="8e71c-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="8e71c-135">Spark Hdınsight kümelerinde kullanılan Jupyter not defterleri, ASCII olmayan karakterler adlarında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e71c-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="8e71c-136">ASCII olmayan dosya adı olan Jupyter kullanıcı Arabirimi aracılığıyla bir dosyayı karşıya yüklemeyi denerseniz, sessizce başarısız olur (diğer bir deyişle, Jupyter, dosyayı karşıya yüklemeyi izin vermiyor ancak görünebilen bir hata ya da throw olmaz).</span><span class="sxs-lookup"><span data-stu-id="8e71c-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="8e71c-137">Daha büyük boyutta not defterlerini yüklenirken hata oluştu</span><span class="sxs-lookup"><span data-stu-id="8e71c-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="8e71c-138">Bir hata görebilirsiniz  **`Error loading notebook`**  daha büyük boyutta not defterlerini yükleme.</span><span class="sxs-lookup"><span data-stu-id="8e71c-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="8e71c-139">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="8e71c-139">**Mitigation:**</span></span>

<span data-ttu-id="8e71c-140">Bu hata alırsanız, bozuk veya kayıp verilerinizi gelmez.</span><span class="sxs-lookup"><span data-stu-id="8e71c-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="8e71c-141">Yine diskte, dizüstü bilgisayarlarda `/var/lib/jupyter`, ve bunlara erişmek için kümeye SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e71c-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="8e71c-142">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8e71c-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="8e71c-143">SSH kullanarak kümeye bağlandıktan sonra not defterlerinizi kümenizden (SCP veya WinSCP kullanarak) yerel makinenize not defterindeki önemli verilerin kaybını önlemek için yedek olarak kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e71c-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="8e71c-144">Bağlantı noktası ağ geçidi üzerinden geçmeden Jupyter erişmek için 8001, headnode içine SSH tüneli kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e71c-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="8e71c-145">Buradan, dizüstü bilgisayarınızı çıktısını temizleyin ve not defterinin boyutu en aza indirmek için yeniden kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8e71c-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="8e71c-146">Bu hata gelecekte tekrarlamasını önlemek için bazı en iyi uygulamaları izlemelisiniz:</span><span class="sxs-lookup"><span data-stu-id="8e71c-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="8e71c-147">Not defteri boyutunu küçük tutmaya önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8e71c-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="8e71c-148">Geri Jupyter için gönderilen bir Spark işleriniz çıktı not defterinde kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8e71c-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="8e71c-149">Bunu Jupyter ile en iyi uygulama genel çalışan kaçınmaktır `.collect()` üzerinde büyük RDD'ın veya dataframes; bir RDD'ın içeriğini peek istiyorsanız, bunun yerine, çalışan göz önünde bulundurun `.take()` veya `.sample()` böylelikle, çıkış çok büyük açılmıyor.</span><span class="sxs-lookup"><span data-stu-id="8e71c-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="8e71c-150">Bir not defteri kaydettiğinizde, ayrıca, Temizle tüm boyutunu azaltmak için hücreleri çıktı.</span><span class="sxs-lookup"><span data-stu-id="8e71c-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="8e71c-151">Not defteri başlangıç beklenenden uzun sürüyor</span><span class="sxs-lookup"><span data-stu-id="8e71c-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="8e71c-152">Jupyter Not Defteri kullanarak Spark Sihirli ilk kod deyiminde birden fazla bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8e71c-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="8e71c-153">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="8e71c-153">**Explanation:**</span></span>

<span data-ttu-id="8e71c-154">Birinci kod hücresini çalıştırdığınızda çünkü bu gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="8e71c-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="8e71c-155">Arka planda bu başlatır oturum yapılandırması ve Spark, SQL ve Hive bağlamları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8e71c-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="8e71c-156">Sonra bu içerikler ayarlayın, ilk ifadesini çalıştırmak ve bu izlenim gösteren deyimi tamamlanması uzun zaman aldı.</span><span class="sxs-lookup"><span data-stu-id="8e71c-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="8e71c-157">Oturum oluşturma Jupyter not defteri zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="8e71c-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="8e71c-158">Spark kümesi kaynaklar yetersiz olduğunda, Jupyter Not Defteri, Spark ve Pyspark tekrar oturum oluşturulmaya çalışılırken zaman aşımı olur.</span><span class="sxs-lookup"><span data-stu-id="8e71c-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="8e71c-159">**Azaltıcı Etkenler:**</span><span class="sxs-lookup"><span data-stu-id="8e71c-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="8e71c-160">Bazı kaynaklar tarafından Spark kümenizdeki boşaltmak:</span><span class="sxs-lookup"><span data-stu-id="8e71c-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="8e71c-161">Diğer Spark not defterlerini kapatın ve durdurmak menüsüne giderek veya dizüstü bilgisayar explorer'ın kapanması tıklatarak durduruluyor.</span><span class="sxs-lookup"><span data-stu-id="8e71c-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="8e71c-162">YARN diğer Spark uygulamalardan durduruluyor.</span><span class="sxs-lookup"><span data-stu-id="8e71c-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="8e71c-163">Başlatılması çalıştığınız dizüstü bilgisayar yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="8e71c-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="8e71c-164">Yeterli kaynaklara oturum şimdi oluşturmak için kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e71c-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="8e71c-165">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8e71c-165">See also</span></span>
* [<span data-ttu-id="8e71c-166">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="8e71c-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8e71c-167">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="8e71c-167">Scenarios</span></span>
* [<span data-ttu-id="8e71c-168">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="8e71c-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8e71c-169">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8e71c-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8e71c-170">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8e71c-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8e71c-171">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="8e71c-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="8e71c-172">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="8e71c-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8e71c-173">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8e71c-173">Create and run applications</span></span>
* [<span data-ttu-id="8e71c-174">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e71c-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8e71c-175">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8e71c-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8e71c-176">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="8e71c-176">Tools and extensions</span></span>
* [<span data-ttu-id="8e71c-177">Spark Scala uygulamaları oluşturmak ve göndermek amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="8e71c-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8e71c-178">Spark uygulamalarında uzaktan hata ayıklamak amacıyla IntelliJ IDEA için HDInsight Araçları Eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="8e71c-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8e71c-179">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="8e71c-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8e71c-180">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="8e71c-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8e71c-181">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="8e71c-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="8e71c-182">Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="8e71c-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8e71c-183">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="8e71c-183">Manage resources</span></span>
* [<span data-ttu-id="8e71c-184">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8e71c-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8e71c-185">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="8e71c-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

