---
title: "aaaUse MapReduce ve Curl hdınsight'ta - Azure Hadoop ile | Microsoft Docs"
description: "Tooremotely çalışma şeklini MapReduce işleri Hadoop ile Hdınsight'ta Curl kullanarak öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="3199f-103">REST kullanarak Hdınsight'ta Hadoop ile MapReduce işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3199f-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="3199f-104">Nasıl Hdınsight kümesinde bir hadoop'ta toouse hello WebHCat REST API toorun MapReduce işleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3199f-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="3199f-105">Curl ham HTTP isteklerini toorun MapReduce işleri kullanarak Hdınsight ile nasıl etkileşim kurabileceğine kullanılan toodemonstrate ' dir.</span><span class="sxs-lookup"><span data-stu-id="3199f-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="3199f-106">Linux tabanlı Hadoop sunucuları kullanarak bilginiz, ancak yeni tooHDInsight, hello bkz [gerekenleri hdınsight'ta Linux tabanlı Hadoop hakkında tooknow](hdinsight-hadoop-linux-information.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3199f-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="3199f-107"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3199f-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="3199f-108">Hdınsight kümesi Hadoop'ta</span><span class="sxs-lookup"><span data-stu-id="3199f-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="3199f-109">Curl</span><span class="sxs-lookup"><span data-stu-id="3199f-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="3199f-110">jq</span><span class="sxs-lookup"><span data-stu-id="3199f-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="3199f-111"><a id="curl"></a>Curl kullanarak MapReduce işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3199f-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="3199f-112">WebHCat ile Curl veya başka bir REST iletişimini kullanırken hello Hdınsight küme yönetici kullanıcı adını ve parolasını sağlayarak hello istekleri kimliğini doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3199f-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="3199f-113">Merhaba kullanılan toosend hello istekleri toohello sunucusu URI bir parçası olarak hello küme adını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3199f-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="3199f-114">Bu bölümdeki Hello komutlar için Değiştir **kullanıcıadı** hello kullanıcı tooauthenticate toohello kümesi ile ve **parola** hello hello kullanıcı hesabının parolasını ile.</span><span class="sxs-lookup"><span data-stu-id="3199f-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="3199f-115">Değiştir **CLUSTERNAME** kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="3199f-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="3199f-116">Merhaba REST API kullanarak korunuyor [temel erişimi kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="3199f-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="3199f-117">Ayrıca, kimlik bilgilerinizi toohello sunucu güvenli bir şekilde gönderilir HTTPS tooensure kullanarak istekleri her zaman yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3199f-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="3199f-118">Bir komut satırından tooyour Hdınsight kümesi bağlanabilir komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3199f-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="3199f-119">JSON izleyen bir yanıt benzer toohello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3199f-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="3199f-120">Bu komutta kullanılan hello parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3199f-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="3199f-121">**-u**: hello kullanıcı adı ve parola kullanılan tooauthenticate hello isteği gösterir</span><span class="sxs-lookup"><span data-stu-id="3199f-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="3199f-122">**-G**: Bu işlem bir GET isteği olduğunu gösterir</span><span class="sxs-lookup"><span data-stu-id="3199f-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="3199f-123">URI, Merhaba başlayan hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, olan hello aynı tüm istekler için.</span><span class="sxs-lookup"><span data-stu-id="3199f-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="3199f-124">toosubmit bir MapReduce işi hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3199f-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="3199f-125">Merhaba URI (/ mapreduce/jar) Hello sonuna bu istek bir sınıftan jar dosyasındaki bir MapReduce işi başlatır WebHCat söyler.</span><span class="sxs-lookup"><span data-stu-id="3199f-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="3199f-126">Bu komutta kullanılan hello parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3199f-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="3199f-127">**-d**: `-G` toohello POST yöntemini hello isteği Varsayılanları şekilde, kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="3199f-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="3199f-128">`-d`gönderilen Merhaba veri değerleri ile Merhaba isteğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3199f-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="3199f-129">**User.Name**: hello komutu çalıştıran hello kullanıcı</span><span class="sxs-lookup"><span data-stu-id="3199f-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="3199f-130">**jar**: sınıf toobe içeren hello jar dosyasını hello konumunu çalıştı</span><span class="sxs-lookup"><span data-stu-id="3199f-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="3199f-131">**sınıf**: Merhaba hello MapReduce mantığı içeren sınıfı</span><span class="sxs-lookup"><span data-stu-id="3199f-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="3199f-132">**arg**: hello bağımsız değişkenleri toobe toohello MapReduce işi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="3199f-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="3199f-133">Bu durumda, hello hello çıktı için kullanılan metin dosyası ve hello dizin girişi</span><span class="sxs-lookup"><span data-stu-id="3199f-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="3199f-134">Bu komut, kullanılan toocheck hello hello işinin durumunu olabilir bir iş kimliği döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3199f-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="3199f-135">{"ID": "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="3199f-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="3199f-136">Merhaba işinin komutu aşağıdaki kullanım hello toocheck hello durumu:</span><span class="sxs-lookup"><span data-stu-id="3199f-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="3199f-137">Hello yerine **JOBID** hello önceki adımda döndürülen hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="3199f-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="3199f-138">Örneğin, hello değeri döndürür `{"id":"job_1415651640909_0026"}`, ardından JOBID olacaktır hello `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="3199f-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="3199f-139">Merhaba işi tamamlandıktan hello durumu döndürülür `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="3199f-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3199f-140">Bu Curl isteği bir JSON belgesi hello işi hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3199f-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="3199f-141">Jq kullanılan tooretrieve yalnızca hello durum değeri.</span><span class="sxs-lookup"><span data-stu-id="3199f-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="3199f-142">Ne zaman hello iş hello durumu değişti çok`SUCCEEDED`, Azure Blob depolama alanından hello iş hello sonuçlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3199f-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="3199f-143">Merhaba `statusdir` hello sorguyla geçirilen parametre hello hello çıkış dosyasının konumunu içerir.</span><span class="sxs-lookup"><span data-stu-id="3199f-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="3199f-144">Bu örnekte, hello konumdur `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="3199f-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="3199f-145">Bu adres hello çıktısını hello hello kümeleri varsayılan depolama depolar `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="3199f-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="3199f-146">Liste ve hello kullanarak bu dosyaları indirmek [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3199f-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="3199f-147">Merhaba hello Azure CLI bloblarından ile çalışma hakkında daha fazla bilgi için bkz: [kullanma hello Azure Storage ile Azure CLI 2.0](../storage/common/storage-azure-cli.md#create-and-manage-blobs) belge.</span><span class="sxs-lookup"><span data-stu-id="3199f-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="3199f-148"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3199f-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3199f-149">Hdınsight'ta MapReduce işleri hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="3199f-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="3199f-150">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="3199f-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="3199f-151">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3199f-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3199f-152">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="3199f-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3199f-153">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="3199f-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="3199f-154">Bu makalede kullanılan hello REST arabirimi hakkında daha fazla bilgi için bkz: Merhaba [WebHCat başvuru](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="3199f-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
