---
title: "Azure Hdınsight kullanarak Spark aaaTroubleshoot | Microsoft Docs"
description: "Apache Spark ve Azure Hdınsight ile çalışma hakkında toocommon soruların yanıtlarını alın."
keywords: "Sorun giderme kılavuzu, ortak sorunları, uygulama yapılandırması, Ambari azure Hdınsight, Spark, SSS,"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="c1404-104">Spark Azure Hdınsight kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="c1404-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="c1404-105">Apache Ambari, Apache Spark yükü ile çalışırken Hello üst sorunları ve bunların çözümleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c1404-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="c1404-106">Spark uygulama kümelerinde Ambari kullanarak nasıl yapılandırırım</span><span class="sxs-lookup"><span data-stu-id="c1404-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="c1404-107">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="c1404-107">Resolution steps</span></span>

<span data-ttu-id="c1404-108">Bu yordam için Hello yapılandırma değerlerini daha önce Hdınsight'ta ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="c1404-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="c1404-109">hangi Spark yapılandırmaları gerekir toobe kümesi ve toowhat değerleri toodetermine bkz [ne bir Spark uygulama OutofMemoryError özel duruma neden olan](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="c1404-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="c1404-110">Kümeleri Hello listesinde seçin **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="c1404-110">In hello list of clusters, select **Spark2**.</span></span>

    ![Küme listeden seçin](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="c1404-112">Select hello **yapılandırmalar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c1404-112">Select hello **Configs** tab.</span></span>

    ![Merhaba yapılandırmalar sekmesini seçin](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="c1404-114">Yapılandırmaları Hello listesinde seçin **özel spark2 varsayılanları**.</span><span class="sxs-lookup"><span data-stu-id="c1404-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Özel spark varsayılanlarını seçin](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="c1404-116">Hello değeri tooadjust, gibi gerektiğini ayarı Ara **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="c1404-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="c1404-117">Bu durumda, değerini hello **4608m** çok yüksek.</span><span class="sxs-lookup"><span data-stu-id="c1404-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Merhaba spark.executor.memory alanı seçin](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="c1404-119">Önerilen hello değeri toohello ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c1404-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="c1404-120">Merhaba değeri **2048m** Bu ayar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="c1404-120">hello value **2048m** is recommended for this setting.</span></span>

    ![Değişiklik değer too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="c1404-122">Merhaba değeri kaydetmek ve hello yapılandırmasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c1404-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="c1404-123">Merhaba araç çubuğunda seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c1404-123">On hello toolbar, select **Save**.</span></span>

    ![Merhaba ayar ve yapılandırmayı kaydedin](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="c1404-125">Tüm yapılandırmaları dikkat etmeniz gereken varsa size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="c1404-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="c1404-126">Not hello öğeleri ve ardından **yine de devam**.</span><span class="sxs-lookup"><span data-stu-id="c1404-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![Select yine de devam etmek](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="c1404-128">Merhaba yapılandırma değişiklikleri hakkında bir not yazın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c1404-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Yaptığınız hello değişiklikler hakkında bir not girin](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="c1404-130">Bir yapılandırma kaydedildiği zaman istenir toorestart hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="c1404-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="c1404-131">Seçin **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="c1404-131">Select **Restart**.</span></span>

    ![Yeniden başlatma seçin](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="c1404-133">Merhaba yeniden onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c1404-133">Confirm hello restart.</span></span>

    ![Select onaylayın tüm yeniden başlatın](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="c1404-135">Çalışan hello işlemleri gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1404-135">You can review hello processes that are running.</span></span>

    ![Çalışan işlemleri gözden geçirin](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="c1404-137">Yapılandırmaları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1404-137">You can add configurations.</span></span> <span data-ttu-id="c1404-138">Yapılandırmaları Hello listesinde seçin **özel spark2 varsayılanları**ve ardından **Özellik Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c1404-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Özellik Seç ekleme](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="c1404-140">Yeni bir özellik tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c1404-140">Define a new property.</span></span> <span data-ttu-id="c1404-141">Merhaba veri türü gibi belirli ayarlar için bir iletişim kutusunu kullanarak tek bir özellik tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1404-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="c1404-142">Ya da her satırda tek bir tanım kullanarak birden çok özellik tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1404-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="c1404-143">Bu örnekte, hello **spark.driver.memory** özellik değeri ile tanımlanmış **4g**.</span><span class="sxs-lookup"><span data-stu-id="c1404-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Yeni özellik tanımlama](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="c1404-145">Merhaba yapılandırmasını kaydetmek ve 6 ve 7. adımda açıklandığı gibi hello hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="c1404-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="c1404-146">Bu değişiklikler, küme çapında ancak hello Spark iş gönderdiğinizde geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="c1404-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="c1404-147">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c1404-147">Additional reading</span></span>

[<span data-ttu-id="c1404-148">Hdınsight kümelerinde Spark iş gönderme</span><span class="sxs-lookup"><span data-stu-id="c1404-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="c1404-149">Spark uygulama kümelerinde Jupyter Not Defteri kullanarak nasıl yapılandırırım</span><span class="sxs-lookup"><span data-stu-id="c1404-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="c1404-150">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="c1404-150">Resolution steps</span></span>

1. <span data-ttu-id="c1404-151">hangi Spark yapılandırmaları gerekir toobe kümesi ve toowhat değerleri toodetermine bkz [ne bir Spark uygulama OutofMemoryError özel duruma neden olan](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="c1404-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="c1404-152">Merhaba, hello sonra hello Jupyter not defteri tablonun ilk hücresini **%% yapılandırma** yönergesi, geçerli JSON biçiminde hello Spark yapılandırmalarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c1404-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="c1404-153">Merhaba gerçek değerleri gerektiği gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c1404-153">Change hello actual values as necessary:</span></span>

    ![Bir yapılandırma ekleyin](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="c1404-155">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c1404-155">Additional reading</span></span>

[<span data-ttu-id="c1404-156">Hdınsight kümelerinde Spark iş gönderme</span><span class="sxs-lookup"><span data-stu-id="c1404-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="c1404-157">Spark uygulama kümelerinde Livy kullanarak nasıl yapılandırırım</span><span class="sxs-lookup"><span data-stu-id="c1404-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="c1404-158">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="c1404-158">Resolution steps</span></span>

1. <span data-ttu-id="c1404-159">hangi Spark yapılandırmaları gerekir toobe kümesi ve toowhat değerleri toodetermine bkz [ne bir Spark uygulama OutofMemoryError özel duruma neden olan](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="c1404-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="c1404-160">REST istemcisi cURL gibi kullanarak Hello Spark uygulama tooLivy gönderin.</span><span class="sxs-lookup"><span data-stu-id="c1404-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="c1404-161">Komut benzer toohello aşağıdaki kullanın.</span><span class="sxs-lookup"><span data-stu-id="c1404-161">Use a command similar toohello following.</span></span> <span data-ttu-id="c1404-162">Merhaba gerçek değerleri gerektiği gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c1404-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="c1404-163">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c1404-163">Additional reading</span></span>

[<span data-ttu-id="c1404-164">Hdınsight kümelerinde Spark iş gönderme</span><span class="sxs-lookup"><span data-stu-id="c1404-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="c1404-165">Kümelerinde nasıl kullanarak uygulama spark gönderme Spark yapılandırırım</span><span class="sxs-lookup"><span data-stu-id="c1404-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="c1404-166">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="c1404-166">Resolution steps</span></span>

1. <span data-ttu-id="c1404-167">hangi Spark yapılandırmaları gerekir toobe kümesi ve toowhat değerleri toodetermine bkz [ne bir Spark uygulama OutofMemoryError özel duruma neden olan](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="c1404-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="c1404-168">Spark Kabuk komut benzer toohello aşağıdakileri kullanarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="c1404-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="c1404-169">Merhaba yapılandırmaları gerçek değerini Hello gerektiği gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c1404-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="c1404-170">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c1404-170">Additional reading</span></span>

[<span data-ttu-id="c1404-171">Hdınsight kümelerinde Spark iş gönderme</span><span class="sxs-lookup"><span data-stu-id="c1404-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="c1404-172">Ne bir Spark uygulama OutofMemoryError özel duruma neden olur</span><span class="sxs-lookup"><span data-stu-id="c1404-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="c1404-173">Ayrıntılı açıklama</span><span class="sxs-lookup"><span data-stu-id="c1404-173">Detailed description</span></span>

<span data-ttu-id="c1404-174">Merhaba Spark uygulama, şu Yakalanmayan Özel durumların türlerini hello ile başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="c1404-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a><span data-ttu-id="c1404-175">Olası neden</span><span class="sxs-lookup"><span data-stu-id="c1404-175">Probable cause</span></span>

<span data-ttu-id="c1404-176">Merhaba büyük olasılıkla bu özel durum yığın bellek yetersiz toohello Java sanal makineler (JVMs) ayrılır nedenidir.</span><span class="sxs-lookup"><span data-stu-id="c1404-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="c1404-177">Bu JVMs yürütücüler veya sürücüler olarak hello Spark uygulama bir parçası olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c1404-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="c1404-178">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="c1404-178">Resolution steps</span></span>

1. <span data-ttu-id="c1404-179">Merhaba veri hello Spark uygulama tanıtıcıları Hello en büyük boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="c1404-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="c1404-180">Merhaba giriş verilerini, hello giriş verilerini ve hello uygulama daha fazla hello ara veri dönüştürülürken üreten hello çıktı verilerini dönüştürme tarafından üretilen hello Ara en büyük boyutunu hello dayalı bir tahmin yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1404-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="c1404-181">İlk resmi tahmin kuramıyorsa bu işlem bir yinelemeli olabilir.</span><span class="sxs-lookup"><span data-stu-id="c1404-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="c1404-182">Toouse bellek ve çekirdek tooaccommodate hello Spark uygulama bakımından yeterli kaynaklara sahip oluşturacağız bu hello Hdınsight küme emin olun.</span><span class="sxs-lookup"><span data-stu-id="c1404-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="c1404-183">Bu hello küme ölçümleri bölümü hello değerleri için hello YARN kullanıcı Arabiriminde görüntüleyerek belirlemek, **kullanılan bellek** vs. **Bellek toplam**, ve **VCores kullanılan** vs. **VCores toplam**.</span><span class="sxs-lookup"><span data-stu-id="c1404-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="c1404-184">Spark aşağıdaki hello % 90'hello kullanılabilir bellek ve çekirdek aşmamalıdır yapılandırmaları tooappropriate değerlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c1404-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="c1404-185">Merhaba değerleri de hello bellek gereksinimlerini hello Spark uygulama içinde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="c1404-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="c1404-186">komutu aşağıdaki hello çalıştırmak tüm yürütücüler tarafından kullanılan tooget hello toplam bellek:</span><span class="sxs-lookup"><span data-stu-id="c1404-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="c1404-187">komutu aşağıdaki hello çalıştırmak hello sürücü tarafından kullanılan tooget hello toplam bellek:</span><span class="sxs-lookup"><span data-stu-id="c1404-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="c1404-188">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c1404-188">Additional reading</span></span>

- [<span data-ttu-id="c1404-189">Spark bellek yönetimine genel bakış</span><span class="sxs-lookup"><span data-stu-id="c1404-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [<span data-ttu-id="c1404-190">Bir Hdınsight kümesi üzerinde Spark uygulamanızın hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="c1404-190">Debug a Spark application on an HDInsight cluster</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

