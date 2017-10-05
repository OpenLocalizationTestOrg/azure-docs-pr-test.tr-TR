---
title: "Curl hdınsight'ta - Azure ile Hadoop Sqoop kullanma | Microsoft Docs"
description: "Sqoop Curl kullanarak hdınsight'a uzaktan göndermek öğrenin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="5094a-103">Curl ile hdınsight'ta Hadoop ile Sqoop işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5094a-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="5094a-104">Hdınsight Hadoop kümesinde Sqoop işlerini çalıştırmak için Curl kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5094a-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="5094a-105">Curl çalıştırmak, izlemek ve Sqoop işleri sonuçları almak için ham HTTP isteklerini kullanarak Hdınsight ile nasıl etkileşim kurabileceğine göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5094a-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="5094a-106">Bu, WebHCat REST (önceki adıyla Templeton da bilinir), Hdınsight küme tarafından sağlanan API'sini kullanarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="5094a-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5094a-107">Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni Hdınsight için, bkz: [Linux'ta Hdınsight kullanma hakkında bilgi](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="5094a-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5094a-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5094a-108">Prerequisites</span></span>
<span data-ttu-id="5094a-109">Bu makaledeki adımları tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="5094a-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="5094a-110">Hdınsight kümesi üzerinde Hadoop (Linux veya Windows tabanlı)</span><span class="sxs-lookup"><span data-stu-id="5094a-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="5094a-111">Curl</span><span class="sxs-lookup"><span data-stu-id="5094a-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="5094a-112">jq</span><span class="sxs-lookup"><span data-stu-id="5094a-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="5094a-113">Curl kullanarak Sqoop işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="5094a-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="5094a-114">Curl’ü veya WebHCat ile başka bir REST iletişimini kullanırken HDInsight küme yöneticisinin kullanıcı adı ve parolasını sağlayarak isteklerin kimliğini doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5094a-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="5094a-115">Ayrıca, sunucuya istek göndermek için kullanılan Tekdüzen Kaynak Tanımlayıcısı’nın (URI) bir parçası olarak küme adını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5094a-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="5094a-116">Bu bölümdeki komutlar için **USERNAME** ifadesini küme kimliğini doğrulayacak kullanıcı ile, **PASSWORD** ifadesini ise kullanıcı hesabının parolası ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5094a-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="5094a-117">**CLUSTERNAME** değerini kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5094a-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="5094a-118">REST API’sinin güvenliği [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication) ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5094a-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="5094a-119">Kimlik bilgilerinizin sunucuya güvenli bir şekilde gönderilmesi için istekleri her zaman Güvenli HTTP (HTTPS) kullanarak yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5094a-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="5094a-120">HDInsight kümenize bağlanabildiğinizi doğrulamak için bir komut satırında aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="5094a-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="5094a-121">Aşağıdakine benzer bir yanıt almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5094a-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="5094a-122">Bu komutta kullanılan parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5094a-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="5094a-123">**-u** - İstek kimliğini doğrulamak için kullanılan kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="5094a-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="5094a-124">**-G** - Bunun bir GET isteği olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="5094a-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="5094a-125">URL'nin başına **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, tüm istekler için aynı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5094a-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="5094a-126">Yol **/status**, sunucu için istek WebHCat (Templeton olarak da bilinir) durumuna döndürmek için olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="5094a-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="5094a-127">Sqoop işi göndermek için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="5094a-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="5094a-128">Bu komutta kullanılan parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5094a-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="5094a-129">**-d** - bu yana `-G` kullanılmaz, istek varsayılan olarak, POST yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5094a-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="5094a-130">`-d`istekle birlikte gönderilen veri değerleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="5094a-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="5094a-131">**User.Name** -komutu çalıştıran kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="5094a-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="5094a-132">**komut** -Sqoop komutun yürütülmesi için.</span><span class="sxs-lookup"><span data-stu-id="5094a-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="5094a-133">**statusdir** -bu iş için durumu yazılır dizin.</span><span class="sxs-lookup"><span data-stu-id="5094a-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="5094a-134">Bu komut, iş durumunu denetlemek için kullanılan bir iş kimliği döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="5094a-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="5094a-135">İş durumunu denetlemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5094a-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="5094a-136">Değiştir **JOBID** önceki adımda döndürülen değer.</span><span class="sxs-lookup"><span data-stu-id="5094a-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="5094a-137">Örneğin, dönüş değeri `{"id":"job_1415651640909_0026"}`, ardından **JOBID** olacaktır `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="5094a-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="5094a-138">İş tamamlandı, durum olacaktır **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="5094a-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5094a-139">Bu Curl isteği iş hakkındaki bilgileri ile bir JavaScript nesne gösterimi (JSON) belgesini döndürür; jq yalnızca durum değeri almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5094a-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="5094a-140">İş durumu olarak değiştirildi sonra **başarılı**, Azure Blob depolama alanından iş sonuçlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5094a-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="5094a-141">`statusdir` Sorguyla geçirilen parametre içeren çıkış dosyasının; bu durumda, konumu **wasb: / / / örnek/curl**.</span><span class="sxs-lookup"><span data-stu-id="5094a-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="5094a-142">Bu adres işinde çıktısını depolar **örnek/curl** Hdınsight küme tarafından kullanılan varsayılan depolama kapsayıcısı üzerinde dizin.</span><span class="sxs-lookup"><span data-stu-id="5094a-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="5094a-143">Liste ve kullanarak bu dosyaları indirmek [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5094a-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="5094a-144">Örneğin, liste dosyalarında için **örnek/curl**, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="5094a-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="5094a-145">Bir dosyayı indirmek için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="5094a-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="5094a-146">Blob içeriyor. kullanarak depolama hesabı adı ya da belirtmeniz gerekir `-a` ve `-k` parametreleri veya kümesi **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_erişim\_anahtar** ortam değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="5094a-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="5094a-147">Bkz: < bir href = "hdınsight-karşıya yükleme-data.md" target = "_blank" daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="5094a-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="5094a-148">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="5094a-148">Limitations</span></span>
* <span data-ttu-id="5094a-149">Toplu export - ile Linux tabanlı Hdınsight, Microsoft SQL Server veya Azure SQL veritabanı için verileri dışa aktarmak için kullanılan Sqoop bağlayıcı toplu eklemeler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="5094a-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="5094a-150">-Kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop, INSERT işlemlerine toplu işleme yerine birden çok eklemeleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5094a-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="5094a-151">Özet</span><span class="sxs-lookup"><span data-stu-id="5094a-151">Summary</span></span>
<span data-ttu-id="5094a-152">Bu belgede gösterildiği gibi çalıştırın, izlemek ve Hdınsight kümenize Sqoop işleri sonuçlarını görüntülemek için ham bir HTTP isteği'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5094a-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="5094a-153">Bu makalede kullanılan REST arabirimi hakkında daha fazla bilgi için bkz: <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API Kılavuzu</a>.</span><span class="sxs-lookup"><span data-stu-id="5094a-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5094a-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5094a-154">Next steps</span></span>
<span data-ttu-id="5094a-155">Hdınsight ile Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="5094a-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="5094a-156">Hdınsight'ta Hadoop ile Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="5094a-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="5094a-157">Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5094a-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5094a-158">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="5094a-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5094a-159">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="5094a-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5094a-160">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="5094a-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


