---
title: "Azure hdınsight'ta aaaUse Livy Spark toosubmit işleri tooSpark kümesinde | Microsoft Docs"
description: "Uzaktan tooan Azure Hdınsight kümesi nasıl toouse Apache Spark REST API toosubmit Spark işlerinin öğrenin."
keywords: Apache spark rest API, livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Apache Spark REST API toosubmit uzak işleri tooan Hdınsight Spark kümesi kullanın

Nasıl toouse Livy, hello Apache Spark kullanılan toosubmit uzak olan REST API tooan Azure Hdınsight Spark kümesinde işleri öğrenin. Ayrıntılı belgeler için bkz: [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).

Livy toorun etkileşimli Spark Kabukları kullanın veya toplu işleri toobe Spark üzerinde çalıştırmak gönderin. Bu makalede Livy toosubmit toplu işleri kullanma hakkında alınmaktadır. Bu makalede Hello parçacıkları cURL toomake REST API çağrıları toohello Livy Spark uç kullanın.

**Ön koşullar:**

* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).

* [cURL](http://curl.haxx.se/). Bu makalede, Hdınsight Spark kümesinde karşı nasıl toomake REST API çağrıları cURL toodemonstrate kullanır.

## <a name="submit-a-livy-spark-batch-job"></a>Livy Spark toplu iş gönderme
Toplu iş göndermeden önce hello uygulama jar hello kümesi ile ilişkili hello küme depolama yüklemeniz gerekir. Kullanabileceğiniz [ **AzCopy**](../storage/common/storage-use-azcopy.md), bir komut satırı yardımcı programı, toodo şekilde. Tooupload verileri kullanabileceğiniz çeşitli istemciler vardır. Onları hakkında daha fazla bilgiyi [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**Örnekler**:

* Merhaba jar dosyasını hello küme depolama (WASB) ise
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Toopass jar filename hello ve girdi dosyası bir parçası olarak classname hello isterseniz (Bu örnekte, girdi.txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Merhaba kümede çalışan Livy Spark toplu işlemler hakkında bilgi edinin
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**Örnekler**:

* Merhaba küme üzerinde çalışan tüm hello Livy Spark toplu tooretrieve istiyorsanız:
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Tooretrieve verilen yığın belirli bir toplu işin istiyorsanız
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Livy Spark toplu işi silme
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**Örnek**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark ve yüksek kullanılabilirlik
Livy hello kümede çalışan Spark işleri için yüksek kullanılabilirlik sağlar. Aşağıda birkaç örnek verilmiştir.

* Uzaktan bir işi gönderdikten sonra hello Livy hizmeti devre dışı kalırsa tooa Spark küme, hello iş toorun hello arka planda devam eder. Livy yedekleme olduğunda hello durumunu hello iş ve raporları geri yükler.
* Hdınsight için Jupyter not defterleri Livy tarafından hello arka güç sağlar. Bir not defteri Spark işi çalışıyor ve hello Livy hizmeti yeniden, hello dizüstü toorun hello kod hücreleri devam eder. 

## <a name="show-me-an-example"></a>Örnek göster
Bu bölümde, biz örnekler toouse Livy Spark toosubmit toplu işi arayın, hello hello işinin ilerlemesini izlemek ve silin. Merhaba Bu örnekte kullandığımız bir geliştirilen hello makalesinde hello uygulamasıdır [bir tek başına Scala uygulama toorun Hdınsight Spark kümesinde oluşturup](hdinsight-apache-spark-create-standalone-application.md). Burada Hello adımları, varsayın:

* Merhaba kümesi ile ilişkili hello uygulama jar toohello depolama hesabı üzerinde önceden kopyaladığınız.
* CuRL, şu adımları çalıştığınız hello bilgisayarda yüklü olması.

Merhaba aşağıdaki adımları gerçekleştirin:

1. Bize Livy Spark hello kümede çalıştığını ilk doğrulayın. Biz toplu çalışan listesini alarak bunu yapabilirsiniz. İlk kez Merhaba Livy kullanarak işi çalıştırıyorsanız, hello çıkış sıfır döndürmelidir.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Aşağıdaki kod parçacığında bir çıktı benzer toohello almanız gerekir:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hello çıkış son satırında hello nasıl diyor fark **toplam: 0**, hiçbir çalışan toplu önerir.

2. Bize toplu iş şimdi gönderin. Aşağıdaki kod parçacığında hello bir girdi dosyası (girdi.txt) toopass hello jar adı ve hello sınıf adı parametre olarak kullanır. Bu adımları bir Windows bilgisayardan çalıştırılıyorsa, girdi dosyası önerilen yaklaşımı hello kullanmaktır.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Merhaba hello dosyasındaki parametreleri **girdi.txt** şu şekilde tanımlanır:
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    Aşağıdaki kod parçacığında bir çıktı benzer toohello görmeniz gerekir:
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Merhaba çıktının son satırında hello nasıl diyor fark **durumu: Başlangıç**. Ayrıca diyor, **kodu: 0**. Burada, **0** hello toplu kimliğidir.

3. Şimdi hello toplu iş kimliğini kullanarak bu belirli toplu hello durumunu Al
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Aşağıdaki kod parçacığında bir çıktı benzer toohello görmeniz gerekir:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Merhaba çıktı şimdi gösterir **durumu: başarılı**, hangi bu hello iş öneren başarıyla tamamlandı.

4. İsterseniz, artık hello toplu silebilirsiniz.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Aşağıdaki kod parçacığında bir çıktı benzer toohello görmeniz gerekir:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Merhaba çıktının son satırında Hello hello toplu başarıyla silindi gösterir. Bir iş çalışırken, silme, hello işi sonlandırır. Başarıyla veya aksi halde, tamamlanmış bir iş silerseniz hello iş bilgilerini tamamen siler.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>Livy Spark Hdınsight 3.5 kümelerinde kullanma

Hdınsight 3.5 küme, varsayılan olarak, yerel dosya yollarını tooaccess örnek veri dosyalarını veya Kavanoz kullanımını devre dışı bırakır. Toouse hello öneririz `wasb://` yerine tooaccess Kavanoz veya örnek veri dosyalarının yolu hello kümeden. Toouse yerel yol istiyorsanız hello Ambari yapılandırma uygun şekilde güncelleştirmeniz gerekir. toodo için:

1. Merhaba küme için toohello Ambari portal gidin. Merhaba Ambari Web kullanıcı Arabirimi, https:// konumunda Hdınsight kümenize kullanılabilir**CLUSTERNAME**. CLUSTERNAME kümenizin hello adı olduğu azurehdidnsight.net.

2. Sol gezinti hello tıklatın **Livy**ve ardından **yapılandırmalar**.

3. Altında **livy varsayılan** hello özellik adı eklemek `livy.file.local-dir-whitelist` ve çok değeri ayarlayın**"/"** tooallow tam erişim toofile sistem istiyorsanız. Tooallow erişim yalnızca tooa belirli dizin istiyorsanız hello yolu toothat dizin hello değeri olarak sağlayın.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Bir küme içinde bir Azure sanal ağı Livy işleri gönderme

Tooan Hdınsight Spark küme bir Azure sanal ağı içinde bağlanıyorsanız, tooLivy hello kümede doğrudan bağlanabilir. Böyle bir durumda Livy uç noktası için URL hello `http://<IP address of hello headnode>:8998/batches`. Burada, **8998** Livy hello küme headnode üzerinde çalıştığı hello bağlantı noktasıdır. Hizmetlere genel olmayan bağlantı noktalarına erişme hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](hdinsight-hadoop-port-settings-for-services.md).

## <a name="troubleshooting"></a>Sorun giderme

Uzak iş gönderme tooSpark kümeleri için Livy kullanırken içine çalışabilir bazı sorunlar şunlardır.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>Bir dış jar hello ek depolama biriminden kullanılması desteklenmez

**Sorun:** Livy Spark işinizi hello ek depolama hesabından hello kümesi ile ilişkili bir dış jar başvuruyorsa, hello işi başarısız olur.

**Çözüm:** bu hello jar istediğiniz toouse hello Hdınsight kümesi ile ilişkili hello varsayılan depolama alanında kullanılabilir olduğundan emin olun.





## <a name="next-step"></a>Sonraki adım

* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

