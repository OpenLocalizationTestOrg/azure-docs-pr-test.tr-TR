---
title: "Azure Hdınsight'ta Apache Spark aaaTroubleshoot sorunları küme | Microsoft Docs"
description: "Azure hdınsight'ta Spark kümeleri ilgili tooApache sorunlar hakkında bilgi edinmek ve nasıl toowork geçici olanlar."
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
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="bc2b6-103">Hdınsight'ta Apache Spark kümesi için bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="bc2b6-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="bc2b6-104">Bu belge, bilinen sorunlar hello Hdınsight Spark genel Önizleme için tüm hello izler.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="bc2b6-105">Etkileşimli oturum Livy sızdırıyor</span><span class="sxs-lookup"><span data-stu-id="bc2b6-105">Livy leaks interactive session</span></span>
<span data-ttu-id="bc2b6-106">Bir etkileşimli oturum hala canlı Livy (Ambari veya tooheadnode 0 sanal makine yeniden başlatma nedeniyle) yeniden başlatıldığında bir etkileşimli iş oturumu sızmasını.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="bc2b6-107">Bu nedenle, yeni işleri can hello kabul edilen durumu takılmış ve başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="bc2b6-108">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="bc2b6-108">**Mitigation:**</span></span>

<span data-ttu-id="bc2b6-109">Aşağıdaki yordam tooworkaround hello sorunu hello kullan:</span><span class="sxs-lookup"><span data-stu-id="bc2b6-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="bc2b6-110">SSH headnode içine.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-110">Ssh into headnode.</span></span> <span data-ttu-id="bc2b6-111">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bc2b6-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bc2b6-112">Komut toofind Merhaba uygulaması aşağıdaki çalışma hello hello etkileşimli işlerin kimliklerini Livy başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="bc2b6-113">Merhaba işleri ile Livy etkileşimli oturum, hello için belirtilen hiçbir açık adları başlatılmış hello varsayılan proje adları Livy olacaktır Jupyter not defteri tarafından başlatılan Livy oturum hello iş adı başlayacak remotesparkmagics_ * ile.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="bc2b6-114">Komut tookill aşağıdaki hello bu işleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="bc2b6-115">Yeni iş çalışmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="bc2b6-116">Spark geçmişi sunucu başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="bc2b6-116">Spark History Server not started</span></span>
<span data-ttu-id="bc2b6-117">Spark geçmişi sunucu bir küme oluşturulduktan sonra otomatik olarak başlatılan bir dosya değil.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="bc2b6-118">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="bc2b6-118">**Mitigation:**</span></span> 

<span data-ttu-id="bc2b6-119">El ile Merhaba geçmişi sunucu Ambari başlatın.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="bc2b6-120">Spark günlük dizini izin sorunu</span><span class="sxs-lookup"><span data-stu-id="bc2b6-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="bc2b6-121">Hdiuser spark-submit işlemiyle gönderdiğinde, bir hata java.io.FileNotFoundException yoktur: /var/log/spark/sparkdriver_hdiuser.log (izni reddedildi) ve hello sürücü günlüğü yazılmadı.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="bc2b6-122">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="bc2b6-122">**Mitigation:**</span></span>

1. <span data-ttu-id="bc2b6-123">Hdiuser toohello Hadoop grubunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="bc2b6-124">777 izinleri üzerinde /var/log/spark Küme oluşturulduktan sonra sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="bc2b6-125">Ambari toobe bir dizin 777 izinlerle kullanarak hello spark günlük konumunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="bc2b6-126">Çalışma spark-gönderme sudo.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="bc2b6-127">Spark Phoenix bağlayıcı desteklenmez</span><span class="sxs-lookup"><span data-stu-id="bc2b6-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="bc2b6-128">Şu anda hello Spark Phoenix bağlayıcı Hdınsight Spark kümesinde ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="bc2b6-129">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="bc2b6-129">**Mitigation:**</span></span>

<span data-ttu-id="bc2b6-130">Merhaba Spark HBase bağlayıcı yerine kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="bc2b6-131">Yönergeler için bkz [nasıl toouse Spark HBase bağlayıcı](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="bc2b6-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="bc2b6-132">TooJupyter not defterlerini ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="bc2b6-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="bc2b6-133">Aşağıda bazı bilinen sorunlar ilgili tooJupyter not defterlerini verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="bc2b6-134">Dizüstü bilgisayarlarla dosya adları ASCII olmayan karakterler</span><span class="sxs-lookup"><span data-stu-id="bc2b6-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="bc2b6-135">Spark Hdınsight kümelerinde kullanılan Jupyter not defterleri, ASCII olmayan karakterler adlarında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="bc2b6-136">Tooupload hello Jupyter ASCII olmayan dosya adı olan kullanıcı Arabirimi üzerinden dosya çalışırsanız, sessizce başarısız olur (diğer bir deyişle, Jupyter olmaz sağlar, hello dosyasını karşıya yükleyin, ancak görünebilen bir hata ya da throw olmaz).</span><span class="sxs-lookup"><span data-stu-id="bc2b6-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="bc2b6-137">Daha büyük boyutta not defterlerini yüklenirken hata oluştu</span><span class="sxs-lookup"><span data-stu-id="bc2b6-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="bc2b6-138">Bir hata görebilirsiniz ** `Error loading notebook` ** daha büyük boyutta not defterlerini yükleme.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="bc2b6-139">**Azaltma:**</span><span class="sxs-lookup"><span data-stu-id="bc2b6-139">**Mitigation:**</span></span>

<span data-ttu-id="bc2b6-140">Bu hata alırsanız, bozuk veya kayıp verilerinizi gelmez.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="bc2b6-141">Yine diskte, dizüstü bilgisayarlarda `/var/lib/jupyter`, ve SSH hello küme tooaccess bunları.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="bc2b6-142">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bc2b6-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="bc2b6-143">SSH kullanarak toohello küme bağlandıktan sonra önemli bilgileri hello Not yedekleme tooprevent hello kaybı olarak (SCP veya WinSCP kullanarak), küme tooyour yerel makineden defterlerinizi kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="bc2b6-144">Bundan sonra SSH tüneli bağlantı noktası 8001 tooaccess Jupyter adresindeki, headnode içine hello ağ geçidi üzerinden geçmeden yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="bc2b6-145">Buradan, dizüstü bilgisayarınızı hello çıktısını temizleyin ve yeniden kaydedin toominimize hello not defterinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="bc2b6-146">tooprevent hello bazı en iyi uygulamaları izlemelidir gelecekte oluşmasını bu hatadan:</span><span class="sxs-lookup"><span data-stu-id="bc2b6-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="bc2b6-147">Önemli tookeep hello dizüstü bilgisayar boyutu küçük değil.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="bc2b6-148">Spark işleriniz tooJupyter hello not defterinde kalıcı geri gönderilen çıktı.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="bc2b6-149">Jupyter ile en iyi uygulama çalıştıran genel tooavoid içinde olduğu `.collect()` üzerinde büyük RDD'ın veya dataframes; bir RDD'in içeriği adresindeki toopeek istiyorsanız, bunun yerine, çalışan göz önünde bulundurun `.take()` veya `.sample()` böylelikle, çıkış çok büyük açılmıyor.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="bc2b6-150">Bir not defteri kaydettiğinizde, ayrıca, Temizle tüm hücreleri tooreduce hello boyutu çıktı.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="bc2b6-151">Not defteri başlangıç beklenenden uzun sürüyor</span><span class="sxs-lookup"><span data-stu-id="bc2b6-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="bc2b6-152">Jupyter Not Defteri kullanarak Spark Sihirli ilk kod deyiminde birden fazla bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="bc2b6-153">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="bc2b6-153">**Explanation:**</span></span>

<span data-ttu-id="bc2b6-154">Merhaba birinci kod hücresini çalıştırdığınızda çünkü bu gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="bc2b6-155">Merhaba arka planda bu başlatır oturum yapılandırması ve Spark, SQL ve Hive bağlamları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="bc2b6-156">Bu içerikler ayarladıktan sonra hello ilk deyimi çalıştırın ve bu hello deyimi uzun süre toocomplete sürdü hello izlenim sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="bc2b6-157">Merhaba oturum oluşturmayı Jupyter not defteri zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="bc2b6-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="bc2b6-158">Spark kümesi kaynaklar yetersiz olduğunda hello Spark ve Pyspark çekirdekler hello Jupyter Not toocreate hello oturum çalışırken zaman aşımına uğrayacağı.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="bc2b6-159">**Azaltıcı Etkenler:**</span><span class="sxs-lookup"><span data-stu-id="bc2b6-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="bc2b6-160">Bazı kaynaklar tarafından Spark kümenizdeki boşaltmak:</span><span class="sxs-lookup"><span data-stu-id="bc2b6-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="bc2b6-161">Diğer Spark not defterlerini toohello giderek kapatın ve durdurmak menüsü veya kapatma hello not defteri Explorer'da tıklatarak durduruluyor.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="bc2b6-162">YARN diğer Spark uygulamalardan durduruluyor.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="bc2b6-163">Yukarı toostart çalıştığınız hello dizüstü yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="bc2b6-164">Yeterli kaynaklara şimdi bir oturum, toocreate kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="bc2b6-165">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bc2b6-165">See also</span></span>
* [<span data-ttu-id="bc2b6-166">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="bc2b6-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="bc2b6-167">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="bc2b6-167">Scenarios</span></span>
* [<span data-ttu-id="bc2b6-168">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="bc2b6-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="bc2b6-169">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="bc2b6-170">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="bc2b6-171">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="bc2b6-172">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="bc2b6-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="bc2b6-173">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-173">Create and run applications</span></span>
* [<span data-ttu-id="bc2b6-174">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="bc2b6-175">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="bc2b6-176">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="bc2b6-176">Tools and extensions</span></span>
* [<span data-ttu-id="bc2b6-177">Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="bc2b6-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="bc2b6-178">Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="bc2b6-179">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="bc2b6-180">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="bc2b6-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="bc2b6-181">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="bc2b6-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="bc2b6-182">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="bc2b6-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="bc2b6-183">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="bc2b6-183">Manage resources</span></span>
* [<span data-ttu-id="bc2b6-184">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="bc2b6-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="bc2b6-185">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="bc2b6-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

