---
title: "aaaUse REST hdınsight'ta - Azure ile Hadoop Pig | Microsoft Docs"
description: "Azure Hdınsight'ta nasıl toouse REST toorun Pig Latin işlerine bir Hadoop küme öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="9c3d1-103">Pig işleri, REST kullanarak Hdınsight'ta Hadoop ile çalıştırın</span><span class="sxs-lookup"><span data-stu-id="9c3d1-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="9c3d1-104">REST istekleri tooan Azure Hdınsight kümesi yaparak toorun Pig Latin nasıl işler öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="9c3d1-105">Curl hello WebHCat REST API kullanarak Hdınsight ile nasıl etkileşim kullanılan toodemonstrate ' dir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="9c3d1-106">Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni tooHDInsight olan, bkz: [Linux tabanlı Hdınsight ipuçları](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="9c3d1-107"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9c3d1-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="9c3d1-108">Azure Hdınsight (Hadoop hdınsight) kümesi (Linux tabanlı veya Windows tabanlı)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9c3d1-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9c3d1-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="9c3d1-111">Curl</span><span class="sxs-lookup"><span data-stu-id="9c3d1-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="9c3d1-112">jq</span><span class="sxs-lookup"><span data-stu-id="9c3d1-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="9c3d1-113"><a id="curl"></a>Curl kullanarak pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9c3d1-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="9c3d1-114">Merhaba REST API aracılığıyla güvenli [temel erişimi kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="9c3d1-115">Her zaman istekleri kimlik bilgilerinizi toohello sunucu güvenli bir şekilde gönderilir Güvenli HTTP (HTTPS) tooensure kullanarak yapın.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="9c3d1-116">Merhaba komutları bu bölümde, kullanırken değiştirin `USERNAME` hello kullanıcı tooauthenticate toohello küme ve Değiştir ile `PASSWORD` hello hello kullanıcı hesabının parolasını ile.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="9c3d1-117">Değiştir `CLUSTERNAME` kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="9c3d1-118">Bir komut satırından tooyour Hdınsight kümesi bağlanabilir komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="9c3d1-119">JSON yanıt aşağıdaki hello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="9c3d1-120">Bu komutta kullanılan hello parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="9c3d1-121">**-u**: hello kullanıcı adı ve parola kullanılan tooauthenticate hello isteği</span><span class="sxs-lookup"><span data-stu-id="9c3d1-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="9c3d1-122">**-G**: Bu isteği bir GET isteği olduğunu gösterir</span><span class="sxs-lookup"><span data-stu-id="9c3d1-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="9c3d1-123">Merhaba URL'sini başlayan hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, olan hello aynı tüm istekler için.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="9c3d1-124">Merhaba yolu **/status**, o hello isteği tooreturn hello WebHCat (Templeton olarak da bilinir) durumunu hello sunucusu için gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="9c3d1-125">Aşağıdaki kod toosubmit Pig Latin iş toohello küme hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="9c3d1-126">Bu komutta kullanılan hello parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="9c3d1-127">**-d**: çünkü `-G` kullanılmaz, hello isteği varsayılan olarak toohello POST yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="9c3d1-128">`-d`gönderilen Merhaba veri değerleri ile Merhaba isteğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="9c3d1-129">**User.Name**: hello komutu çalıştıran hello kullanıcı</span><span class="sxs-lookup"><span data-stu-id="9c3d1-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="9c3d1-130">**yürütme**: Pig Latin deyimleri tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="9c3d1-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="9c3d1-131">**statusdir**: Bu iş için durumu hello hello dizin yazılır</span><span class="sxs-lookup"><span data-stu-id="9c3d1-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="9c3d1-132">Pig Latin deyimlerinde Hello alanları tarafından hello değiştirilir fark `+` karakter Curl ile kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="9c3d1-133">Bu komut, kullanılan toocheck hello hello işinin durumunu örneğin olabilir bir iş kimliği döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="9c3d1-134">Merhaba işinin komutu aşağıdaki kullanım hello toocheck hello durumu</span><span class="sxs-lookup"><span data-stu-id="9c3d1-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="9c3d1-135">Değiştir `JOBID` hello önceki adımda döndürülen hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="9c3d1-136">Örneğin, hello değeri döndürür `{"id":"job_1415651640909_0026"}`, ardından `JOBID` olan `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="9c3d1-137">Merhaba işi tamamlanmadan hello durumu varsa, **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9c3d1-138">JavaScript nesne gösterimi (JSON) belge hello iş ve jq hakkında bilgi döndürür kullanılan tooretrieve olan bu Curl isteği yalnızca hello durum değeri.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="9c3d1-139"><a id="results"></a>Sonuçları Görüntüle</span><span class="sxs-lookup"><span data-stu-id="9c3d1-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="9c3d1-140">Ne zaman hello iş hello durumu değişti çok**başarılı**, hello iş hello sonuçlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="9c3d1-141">Merhaba `statusdir` hello sorguyla geçirilen parametre içeren hello çıkış dosyasının; bu durumda, hello konumu `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="9c3d1-142">Hdınsight Azure Storage veya Azure Data Lake Store hello varsayılan veri deposu olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="9c3d1-143">Hangisinin bağlı olarak kullandığınız hello verilerini çeşitli şekillerde tooget vardır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="9c3d1-144">Daha fazla bilgi için hello hello depolama bölümüne bakın [Linux tabanlı Hdınsight bilgi](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) belge.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="9c3d1-145"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="9c3d1-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="9c3d1-146">Bu belgede gösterildiği gibi Hdınsight kümesinde bir ham HTTP isteği toorun, İzleyici ve Pig işleri görüntüle hello sonucu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="9c3d1-147">Bu makalede kullanılan hello REST arabirimi hakkında daha fazla bilgi için bkz: Merhaba [WebHCat başvuru](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="9c3d1-148"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c3d1-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9c3d1-149">Hdınsight Pig hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="9c3d1-150">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="9c3d1-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="9c3d1-151">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="9c3d1-152">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="9c3d1-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9c3d1-153">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="9c3d1-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
