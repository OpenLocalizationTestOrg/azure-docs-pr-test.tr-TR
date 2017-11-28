---
title: "aaaUse Hadoop Sqoop Curl hdınsight'ta - Azure ile | Microsoft Docs"
description: "Nasıl tooremotely gönderme Curl kullanarak Sqoop işleri tooHDInsight öğrenin."
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
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="3478e-103">Curl ile hdınsight'ta Hadoop ile Sqoop işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3478e-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="3478e-104">Bir Hadoop toouse Curl toorun Sqoop işlerine Hdınsight'ta nasıl küme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3478e-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="3478e-105">Curl ham HTTP isteklerini toorun, İzleyici ve Sqoop işleri alma hello sonuçlarını kullanarak Hdınsight ile nasıl etkileşim kurabileceğine kullanılan toodemonstrate ' dir.</span><span class="sxs-lookup"><span data-stu-id="3478e-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="3478e-106">Bu, hello WebHCat REST Hdınsight küme tarafından sağlanan API (önceki adıyla Templeton da bilinir) kullanarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="3478e-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3478e-107">Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni tooHDInsight olan, bkz: [Linux'ta Hdınsight kullanma hakkında bilgi](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="3478e-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3478e-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3478e-108">Prerequisites</span></span>
<span data-ttu-id="3478e-109">Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="3478e-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="3478e-110">Hdınsight kümesi üzerinde Hadoop (Linux veya Windows tabanlı)</span><span class="sxs-lookup"><span data-stu-id="3478e-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="3478e-111">Curl</span><span class="sxs-lookup"><span data-stu-id="3478e-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="3478e-112">jq</span><span class="sxs-lookup"><span data-stu-id="3478e-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="3478e-113">Curl kullanarak Sqoop işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="3478e-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="3478e-114">Curl'ü veya başka bir REST iletişimini WebHCat ile kullanırken, hello kullanıcı adı ve parola hello Hdınsight küme yöneticisinin sağlayarak hello istekleri kimliğini doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3478e-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="3478e-115">Merhaba Tekdüzen Kaynak Tanımlayıcısı (URI) bir parçası toosend hello istekleri toohello sunucu kullanılan gibi hello küme adını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3478e-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="3478e-116">Bu bölümdeki Hello komutlar için Değiştir **kullanıcıadı** hello kullanıcı tooauthenticate toohello küme ve Değiştir **parola** hello hello kullanıcı hesabının parolasını ile.</span><span class="sxs-lookup"><span data-stu-id="3478e-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="3478e-117">Değiştir **CLUSTERNAME** kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="3478e-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="3478e-118">Merhaba REST API aracılığıyla güvenli [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="3478e-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="3478e-119">Her zaman güvenli HTTP (toohelp olun kimlik bilgilerinizi toohello sunucu güvenli bir şekilde gönderilir HTTPS) kullanarak istekleri yapmanız.</span><span class="sxs-lookup"><span data-stu-id="3478e-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="3478e-120">Bir komut satırından tooyour Hdınsight kümesi bağlanabilir komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3478e-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="3478e-121">Yanıt benzer toohello aşağıdaki almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3478e-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="3478e-122">Bu komutta kullanılan hello parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3478e-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="3478e-123">**-u** -hello kullanıcı adı ve parola kullanılan tooauthenticate hello isteği.</span><span class="sxs-lookup"><span data-stu-id="3478e-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="3478e-124">**-G** - Bunun bir GET isteği olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="3478e-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="3478e-125">Merhaba URL'sini başlayan hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, aynı tüm istekler için hello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3478e-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="3478e-126">Merhaba yolu **/status**, o hello isteği tooreturn WebHCat (Templeton olarak da bilinir) durumunu hello sunucusu için gösterir.</span><span class="sxs-lookup"><span data-stu-id="3478e-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="3478e-127">Toosubmit sqoop işi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3478e-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="3478e-128">Bu komutta kullanılan hello parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3478e-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="3478e-129">**-d** - bu yana `-G` kullanılmaz, hello isteği varsayılan olarak toohello POST yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3478e-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="3478e-130">`-d`gönderilen Merhaba veri değerleri ile Merhaba isteğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3478e-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="3478e-131">**User.Name** -hello komutu çalıştıran hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="3478e-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="3478e-132">**komut** -Sqoop komutu tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="3478e-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="3478e-133">**statusdir** -bu iş için durumu hello hello dizinine yazılacak.</span><span class="sxs-lookup"><span data-stu-id="3478e-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="3478e-134">Bu komut, kullanılan toocheck hello hello işinin durumunu olabilir bir iş kimliği döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="3478e-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="3478e-135">Merhaba işinin komutu aşağıdaki kullanım hello toocheck hello durumu.</span><span class="sxs-lookup"><span data-stu-id="3478e-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="3478e-136">Değiştir **JOBID** hello önceki adımda döndürülen hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="3478e-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="3478e-137">Örneğin, hello değeri döndürür `{"id":"job_1415651640909_0026"}`, ardından **JOBID** olacaktır `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="3478e-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="3478e-138">Merhaba işi tamamlandı, hello durumu olacaktır **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="3478e-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3478e-139">Bu Curl istek hello işi hakkındaki bilgileri ile bir JavaScript nesne gösterimi (JSON) belgesini döndürür; jq kullanılan tooretrieve yalnızca hello durum değeri.</span><span class="sxs-lookup"><span data-stu-id="3478e-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="3478e-140">Merhaba işin Hello durumu çok değişti sonra**başarılı**, Azure Blob depolama alanından hello iş hello sonuçlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3478e-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="3478e-141">Merhaba `statusdir` hello sorguyla geçirilen parametre içeren hello çıkış dosyasının; bu durumda, hello konumu **wasb: / / / örnek/curl**.</span><span class="sxs-lookup"><span data-stu-id="3478e-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="3478e-142">Bu adresi hello hello çıktı hello işinin saklar **örnek/curl** Hdınsight küme tarafından kullanılan hello varsayılan depolama kapsayıcısı üzerinde dizin.</span><span class="sxs-lookup"><span data-stu-id="3478e-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="3478e-143">Liste ve hello kullanarak bu dosyaları indirmek [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3478e-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="3478e-144">Örneğin, içinde toolist dosyaları **örnek/curl**, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3478e-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="3478e-145">bir dosya toodownload hello aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="3478e-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="3478e-146">Merhaba blob içeriyor. hello kullanarak hello depolama hesabı adı ya da belirtmeniz gerekir `-a` ve `-k` parametreleri veya kümesi hello **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_erişim\_anahtar** ortam değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="3478e-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="3478e-147">Bkz: < bir href = "hdınsight-karşıya yükleme-data.md" target = "_blank" daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3478e-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="3478e-148">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="3478e-148">Limitations</span></span>
* <span data-ttu-id="3478e-149">Toplu export - ile Linux tabanlı Hdınsight, hello Sqoop kullanılan bağlayıcı tooexport veri tooMicrosoft SQL Server ya da Azure SQL veritabanı toplu eklemeler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="3478e-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="3478e-150">-Hello kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop hello INSERT işlemlerine toplu işleme yerine birden çok eklemeleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3478e-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="3478e-151">Özet</span><span class="sxs-lookup"><span data-stu-id="3478e-151">Summary</span></span>
<span data-ttu-id="3478e-152">Bu belgede gösterildiği gibi Hdınsight kümesinde bir ham HTTP isteği toorun, İzleyici ve Sqoop işlerin hello sonuçları görüntüle kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3478e-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="3478e-153">Bu makalede kullanılan hello REST arabirimi hakkında daha fazla bilgi için bkz: Merhaba <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API Kılavuzu</a>.</span><span class="sxs-lookup"><span data-stu-id="3478e-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3478e-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3478e-154">Next steps</span></span>
<span data-ttu-id="3478e-155">Hdınsight ile Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="3478e-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="3478e-156">Hdınsight'ta Hadoop ile Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="3478e-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="3478e-157">Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3478e-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3478e-158">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="3478e-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3478e-159">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="3478e-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="3478e-160">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="3478e-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


