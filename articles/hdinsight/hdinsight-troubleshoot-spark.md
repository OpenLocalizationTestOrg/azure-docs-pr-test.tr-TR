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
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Spark Azure Hdınsight kullanarak sorun giderme

Apache Ambari, Apache Spark yükü ile çalışırken Hello üst sorunları ve bunların çözümleri hakkında bilgi edinin.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>Spark uygulama kümelerinde Ambari kullanarak nasıl yapılandırırım

### <a name="resolution-steps"></a>Çözüm adımları

Bu yordam için Hello yapılandırma değerlerini daha önce Hdınsight'ta ayarlandı. hangi Spark yapılandırmaları gerekir toobe kümesi ve toowhat değerleri toodetermine bkz [ne bir Spark uygulama OutofMemoryError özel duruma neden olan](#what-causes-a-spark-application-outofmemoryerror-exception). 

1. Kümeleri Hello listesinde seçin **Spark2**.

    ![Küme listeden seçin](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. Select hello **yapılandırmalar** sekmesi.

    ![Merhaba yapılandırmalar sekmesini seçin](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. Yapılandırmaları Hello listesinde seçin **özel spark2 varsayılanları**.

    ![Özel spark varsayılanlarını seçin](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. Hello değeri tooadjust, gibi gerektiğini ayarı Ara **spark.executor.memory**. Bu durumda, değerini hello **4608m** çok yüksek.

    ![Merhaba spark.executor.memory alanı seçin](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. Önerilen hello değeri toohello ayarı ayarlayın. Merhaba değeri **2048m** Bu ayar için önerilir.

    ![Değişiklik değer too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Merhaba değeri kaydetmek ve hello yapılandırmasını kaydedin. Merhaba araç çubuğunda seçin **kaydetmek**.

    ![Merhaba ayar ve yapılandırmayı kaydedin](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    Tüm yapılandırmaları dikkat etmeniz gereken varsa size bildirilir. Not hello öğeleri ve ardından **yine de devam**. 

    ![Select yine de devam etmek](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Merhaba yapılandırma değişiklikleri hakkında bir not yazın ve ardından **kaydetmek**.

    ![Yaptığınız hello değişiklikler hakkında bir not girin](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. Bir yapılandırma kaydedildiği zaman istenir toorestart hello hizmet. Seçin **yeniden**.

    ![Yeniden başlatma seçin](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Merhaba yeniden onaylayın.

    ![Select onaylayın tüm yeniden başlatın](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    Çalışan hello işlemleri gözden geçirebilirsiniz.

    ![Çalışan işlemleri gözden geçirin](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. Yapılandırmaları ekleyebilirsiniz. Yapılandırmaları Hello listesinde seçin **özel spark2 varsayılanları**ve ardından **Özellik Ekle**.

    ![Özellik Seç ekleme](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. Yeni bir özellik tanımlayın. Merhaba veri türü gibi belirli ayarlar için bir iletişim kutusunu kullanarak tek bir özellik tanımlayabilirsiniz. Ya da her satırda tek bir tanım kullanarak birden çok özellik tanımlayabilirsiniz. 

    Bu örnekte, hello **spark.driver.memory** özellik değeri ile tanımlanmış **4g**.

    ![Yeni özellik tanımlama](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Merhaba yapılandırmasını kaydetmek ve 6 ve 7. adımda açıklandığı gibi hello hizmetini yeniden başlatın.

Bu değişiklikler, küme çapında ancak hello Spark iş gönderdiğinizde geçersiz kılınabilir.

### <a name="additional-reading"></a>Ek kaynaklar

[Hdınsight kümelerinde Spark iş gönderme](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>Spark uygulama kümelerinde Jupyter Not Defteri kullanarak nasıl yapılandırırım

### <a name="resolution-steps"></a>Çözüm adımları

1. hangi Spark yapılandırmaları gerekir toobe kümesi ve toowhat değerleri toodetermine bkz [ne bir Spark uygulama OutofMemoryError özel duruma neden olan](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Merhaba, hello sonra hello Jupyter not defteri tablonun ilk hücresini **%% yapılandırma** yönergesi, geçerli JSON biçiminde hello Spark yapılandırmalarını belirtin. Merhaba gerçek değerleri gerektiği gibi değiştirin:

    ![Bir yapılandırma ekleyin](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>Ek kaynaklar

[Hdınsight kümelerinde Spark iş gönderme](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>Spark uygulama kümelerinde Livy kullanarak nasıl yapılandırırım

### <a name="resolution-steps"></a>Çözüm adımları

1. hangi Spark yapılandırmaları gerekir toobe kümesi ve toowhat değerleri toodetermine bkz [ne bir Spark uygulama OutofMemoryError özel duruma neden olan](#what-causes-a-spark-application-outofmemoryerror-exception). 

2. REST istemcisi cURL gibi kullanarak Hello Spark uygulama tooLivy gönderin. Komut benzer toohello aşağıdaki kullanın. Merhaba gerçek değerleri gerektiği gibi değiştirin:

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>Ek kaynaklar

[Hdınsight kümelerinde Spark iş gönderme](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>Kümelerinde nasıl kullanarak uygulama spark gönderme Spark yapılandırırım

### <a name="resolution-steps"></a>Çözüm adımları

1. hangi Spark yapılandırmaları gerekir toobe kümesi ve toowhat değerleri toodetermine bkz [ne bir Spark uygulama OutofMemoryError özel duruma neden olan](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Spark Kabuk komut benzer toohello aşağıdakileri kullanarak başlatın. Merhaba yapılandırmaları gerçek değerini Hello gerektiği gibi değiştirin: 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>Ek kaynaklar

[Hdınsight kümelerinde Spark iş gönderme](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>Ne bir Spark uygulama OutofMemoryError özel duruma neden olur

### <a name="detailed-description"></a>Ayrıntılı açıklama

Merhaba Spark uygulama, şu Yakalanmayan Özel durumların türlerini hello ile başarısız olur:

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

### <a name="probable-cause"></a>Olası neden

Merhaba büyük olasılıkla bu özel durum yığın bellek yetersiz toohello Java sanal makineler (JVMs) ayrılır nedenidir. Bu JVMs yürütücüler veya sürücüler olarak hello Spark uygulama bir parçası olarak başlatılır. 

### <a name="resolution-steps"></a>Çözüm adımları

1. Merhaba veri hello Spark uygulama tanıtıcıları Hello en büyük boyutunu belirler. Merhaba giriş verilerini, hello giriş verilerini ve hello uygulama daha fazla hello ara veri dönüştürülürken üreten hello çıktı verilerini dönüştürme tarafından üretilen hello Ara en büyük boyutunu hello dayalı bir tahmin yapabilirsiniz. İlk resmi tahmin kuramıyorsa bu işlem bir yinelemeli olabilir. 

2. Toouse bellek ve çekirdek tooaccommodate hello Spark uygulama bakımından yeterli kaynaklara sahip oluşturacağız bu hello Hdınsight küme emin olun. Bu hello küme ölçümleri bölümü hello değerleri için hello YARN kullanıcı Arabiriminde görüntüleyerek belirlemek, **kullanılan bellek** vs. **Bellek toplam**, ve **VCores kullanılan** vs. **VCores toplam**.

3. Spark aşağıdaki hello % 90'hello kullanılabilir bellek ve çekirdek aşmamalıdır yapılandırmaları tooappropriate değerlerini ayarlayın. Merhaba değerleri de hello bellek gereksinimlerini hello Spark uygulama içinde olmalıdır: 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    komutu aşağıdaki hello çalıştırmak tüm yürütücüler tarafından kullanılan tooget hello toplam bellek: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    komutu aşağıdaki hello çalıştırmak hello sürücü tarafından kullanılan tooget hello toplam bellek:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>Ek kaynaklar

- [Spark bellek yönetimine genel bakış](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [Bir Hdınsight kümesi üzerinde Spark uygulamanızın hatalarını ayıklama](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

