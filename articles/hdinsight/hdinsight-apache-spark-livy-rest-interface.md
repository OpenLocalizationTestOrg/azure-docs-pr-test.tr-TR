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
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="e8eb5-104">Apache Spark REST API toosubmit uzak işleri tooan Hdınsight Spark kümesi kullanın</span><span class="sxs-lookup"><span data-stu-id="e8eb5-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="e8eb5-105">Nasıl toouse Livy, hello Apache Spark kullanılan toosubmit uzak olan REST API tooan Azure Hdınsight Spark kümesinde işleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="e8eb5-106">Ayrıntılı belgeler için bkz: [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="e8eb5-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="e8eb5-107">Livy toorun etkileşimli Spark Kabukları kullanın veya toplu işleri toobe Spark üzerinde çalıştırmak gönderin.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="e8eb5-108">Bu makalede Livy toosubmit toplu işleri kullanma hakkında alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="e8eb5-109">Bu makalede Hello parçacıkları cURL toomake REST API çağrıları toohello Livy Spark uç kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="e8eb5-110">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="e8eb5-110">**Prerequisites:**</span></span>

* <span data-ttu-id="e8eb5-111">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e8eb5-112">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e8eb5-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="e8eb5-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="e8eb5-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="e8eb5-114">Bu makalede, Hdınsight Spark kümesinde karşı nasıl toomake REST API çağrıları cURL toodemonstrate kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="e8eb5-115">Livy Spark toplu iş gönderme</span><span class="sxs-lookup"><span data-stu-id="e8eb5-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="e8eb5-116">Toplu iş göndermeden önce hello uygulama jar hello kümesi ile ilişkili hello küme depolama yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="e8eb5-117">Kullanabileceğiniz [ **AzCopy**](../storage/common/storage-use-azcopy.md), bir komut satırı yardımcı programı, toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="e8eb5-118">Tooupload verileri kullanabileceğiniz çeşitli istemciler vardır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="e8eb5-119">Onları hakkında daha fazla bilgiyi [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="e8eb5-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="e8eb5-120">**Örnekler**:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-120">**Examples**:</span></span>

* <span data-ttu-id="e8eb5-121">Merhaba jar dosyasını hello küme depolama (WASB) ise</span><span class="sxs-lookup"><span data-stu-id="e8eb5-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="e8eb5-122">Toopass jar filename hello ve girdi dosyası bir parçası olarak classname hello isterseniz (Bu örnekte, girdi.txt)</span><span class="sxs-lookup"><span data-stu-id="e8eb5-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="e8eb5-123">Merhaba kümede çalışan Livy Spark toplu işlemler hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="e8eb5-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="e8eb5-124">**Örnekler**:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-124">**Examples**:</span></span>

* <span data-ttu-id="e8eb5-125">Merhaba küme üzerinde çalışan tüm hello Livy Spark toplu tooretrieve istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="e8eb5-126">Tooretrieve verilen yığın belirli bir toplu işin istiyorsanız</span><span class="sxs-lookup"><span data-stu-id="e8eb5-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="e8eb5-127">Livy Spark toplu işi silme</span><span class="sxs-lookup"><span data-stu-id="e8eb5-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="e8eb5-128">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="e8eb5-129">Livy Spark ve yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="e8eb5-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="e8eb5-130">Livy hello kümede çalışan Spark işleri için yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="e8eb5-131">Aşağıda birkaç örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="e8eb5-132">Uzaktan bir işi gönderdikten sonra hello Livy hizmeti devre dışı kalırsa tooa Spark küme, hello iş toorun hello arka planda devam eder.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="e8eb5-133">Livy yedekleme olduğunda hello durumunu hello iş ve raporları geri yükler.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="e8eb5-134">Hdınsight için Jupyter not defterleri Livy tarafından hello arka güç sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="e8eb5-135">Bir not defteri Spark işi çalışıyor ve hello Livy hizmeti yeniden, hello dizüstü toorun hello kod hücreleri devam eder.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="e8eb5-136">Örnek göster</span><span class="sxs-lookup"><span data-stu-id="e8eb5-136">Show me an example</span></span>
<span data-ttu-id="e8eb5-137">Bu bölümde, biz örnekler toouse Livy Spark toosubmit toplu işi arayın, hello hello işinin ilerlemesini izlemek ve silin.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="e8eb5-138">Merhaba Bu örnekte kullandığımız bir geliştirilen hello makalesinde hello uygulamasıdır [bir tek başına Scala uygulama toorun Hdınsight Spark kümesinde oluşturup](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="e8eb5-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="e8eb5-139">Burada Hello adımları, varsayın:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-139">hello steps here assume that:</span></span>

* <span data-ttu-id="e8eb5-140">Merhaba kümesi ile ilişkili hello uygulama jar toohello depolama hesabı üzerinde önceden kopyaladığınız.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="e8eb5-141">CuRL, şu adımları çalıştığınız hello bilgisayarda yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="e8eb5-142">Merhaba aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="e8eb5-143">Bize Livy Spark hello kümede çalıştığını ilk doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="e8eb5-144">Biz toplu çalışan listesini alarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="e8eb5-145">İlk kez Merhaba Livy kullanarak işi çalıştırıyorsanız, hello çıkış sıfır döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="e8eb5-146">Aşağıdaki kod parçacığında bir çıktı benzer toohello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="e8eb5-147">Hello çıkış son satırında hello nasıl diyor fark **toplam: 0**, hiçbir çalışan toplu önerir.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="e8eb5-148">Bize toplu iş şimdi gönderin.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-148">Let us now submit a batch job.</span></span> <span data-ttu-id="e8eb5-149">Aşağıdaki kod parçacığında hello bir girdi dosyası (girdi.txt) toopass hello jar adı ve hello sınıf adı parametre olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="e8eb5-150">Bu adımları bir Windows bilgisayardan çalıştırılıyorsa, girdi dosyası önerilen yaklaşımı hello kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="e8eb5-151">Merhaba hello dosyasındaki parametreleri **girdi.txt** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="e8eb5-152">Aşağıdaki kod parçacığında bir çıktı benzer toohello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-152">You should see an output similar toohello  following snippet:</span></span>
   
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
   
    <span data-ttu-id="e8eb5-153">Merhaba çıktının son satırında hello nasıl diyor fark **durumu: Başlangıç**.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="e8eb5-154">Ayrıca diyor, **kodu: 0**.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-154">It also says, **id:0**.</span></span> <span data-ttu-id="e8eb5-155">Burada, **0** hello toplu kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="e8eb5-156">Şimdi hello toplu iş kimliğini kullanarak bu belirli toplu hello durumunu Al</span><span class="sxs-lookup"><span data-stu-id="e8eb5-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="e8eb5-157">Aşağıdaki kod parçacığında bir çıktı benzer toohello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="e8eb5-158">Merhaba çıktı şimdi gösterir **durumu: başarılı**, hangi bu hello iş öneren başarıyla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="e8eb5-159">İsterseniz, artık hello toplu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="e8eb5-160">Aşağıdaki kod parçacığında bir çıktı benzer toohello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="e8eb5-161">Merhaba çıktının son satırında Hello hello toplu başarıyla silindi gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="e8eb5-162">Bir iş çalışırken, silme, hello işi sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="e8eb5-163">Başarıyla veya aksi halde, tamamlanmış bir iş silerseniz hello iş bilgilerini tamamen siler.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="e8eb5-164">Livy Spark Hdınsight 3.5 kümelerinde kullanma</span><span class="sxs-lookup"><span data-stu-id="e8eb5-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="e8eb5-165">Hdınsight 3.5 küme, varsayılan olarak, yerel dosya yollarını tooaccess örnek veri dosyalarını veya Kavanoz kullanımını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="e8eb5-166">Toouse hello öneririz `wasb://` yerine tooaccess Kavanoz veya örnek veri dosyalarının yolu hello kümeden.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="e8eb5-167">Toouse yerel yol istiyorsanız hello Ambari yapılandırma uygun şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="e8eb5-168">toodo için:</span><span class="sxs-lookup"><span data-stu-id="e8eb5-168">toodo so:</span></span>

1. <span data-ttu-id="e8eb5-169">Merhaba küme için toohello Ambari portal gidin.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="e8eb5-170">Merhaba Ambari Web kullanıcı Arabirimi, https:// konumunda Hdınsight kümenize kullanılabilir**CLUSTERNAME**. CLUSTERNAME kümenizin hello adı olduğu azurehdidnsight.net.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="e8eb5-171">Sol gezinti hello tıklatın **Livy**ve ardından **yapılandırmalar**.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="e8eb5-172">Altında **livy varsayılan** hello özellik adı eklemek `livy.file.local-dir-whitelist` ve çok değeri ayarlayın**"/"** tooallow tam erişim toofile sistem istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="e8eb5-173">Tooallow erişim yalnızca tooa belirli dizin istiyorsanız hello yolu toothat dizin hello değeri olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="e8eb5-174">Bir küme içinde bir Azure sanal ağı Livy işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="e8eb5-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="e8eb5-175">Tooan Hdınsight Spark küme bir Azure sanal ağı içinde bağlanıyorsanız, tooLivy hello kümede doğrudan bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="e8eb5-176">Böyle bir durumda Livy uç noktası için URL hello `http://<IP address of hello headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="e8eb5-177">Burada, **8998** Livy hello küme headnode üzerinde çalıştığı hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="e8eb5-178">Hizmetlere genel olmayan bağlantı noktalarına erişme hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="e8eb5-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e8eb5-179">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e8eb5-179">Troubleshooting</span></span>

<span data-ttu-id="e8eb5-180">Uzak iş gönderme tooSpark kümeleri için Livy kullanırken içine çalışabilir bazı sorunlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="e8eb5-181">Bir dış jar hello ek depolama biriminden kullanılması desteklenmez</span><span class="sxs-lookup"><span data-stu-id="e8eb5-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="e8eb5-182">**Sorun:** Livy Spark işinizi hello ek depolama hesabından hello kümesi ile ilişkili bir dış jar başvuruyorsa, hello işi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="e8eb5-183">**Çözüm:** bu hello jar istediğiniz toouse hello Hdınsight kümesi ile ilişkili hello varsayılan depolama alanında kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e8eb5-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="e8eb5-184">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="e8eb5-184">Next step</span></span>

* [<span data-ttu-id="e8eb5-185">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="e8eb5-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e8eb5-186">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="e8eb5-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

