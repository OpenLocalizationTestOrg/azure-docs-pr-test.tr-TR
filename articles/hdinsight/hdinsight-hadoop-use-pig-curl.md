---
title: "Hadoop Pig hdınsight'ta - Azure REST ile kullanma | Microsoft Docs"
description: "Azure Hdınsight Hadoop kümesinde Pig Latin işlerini çalıştırmak için REST kullanmayı öğrenin."
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
ms.openlocfilehash: a86864a779b0de1c6d5669cfbba0f3e1a27f1ff1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="21b4d-103">Pig işleri, REST kullanarak Hdınsight'ta Hadoop ile çalıştırın</span><span class="sxs-lookup"><span data-stu-id="21b4d-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="21b4d-104">Azure Hdınsight kümesi için REST istekleri yaparak pig Latin işleri çalıştırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="21b4d-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="21b4d-105">Curl WebHCat REST API kullanarak Hdınsight ile nasıl etkileşim göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21b4d-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="21b4d-106">Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni Hdınsight için, bkz: [Linux tabanlı Hdınsight ipuçları](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="21b4d-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="21b4d-107"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="21b4d-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="21b4d-108">Azure Hdınsight (Hadoop hdınsight) kümesi (Linux tabanlı veya Windows tabanlı)</span><span class="sxs-lookup"><span data-stu-id="21b4d-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="21b4d-109">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="21b4d-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="21b4d-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="21b4d-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="21b4d-111">Curl</span><span class="sxs-lookup"><span data-stu-id="21b4d-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="21b4d-112">jq</span><span class="sxs-lookup"><span data-stu-id="21b4d-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="21b4d-113"><a id="curl"></a>Curl kullanarak pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="21b4d-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="21b4d-114">REST API aracılığıyla güvenli [temel erişimi kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="21b4d-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="21b4d-115">Her zaman istekleri kimlik bilgilerinizin sunucuya güvenli bir şekilde gönderildiğinden emin olmak için Güvenli HTTP (HTTPS) kullanarak yapın.</span><span class="sxs-lookup"><span data-stu-id="21b4d-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="21b4d-116">Bu bölümdeki komutlar kullanırken, Değiştir `USERNAME` küme kimliğini ve değiştirmek için kullanıcıyla `PASSWORD` kullanıcı hesabı için parola ile.</span><span class="sxs-lookup"><span data-stu-id="21b4d-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="21b4d-117">`CLUSTERNAME` değerini kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="21b4d-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="21b4d-118">HDInsight kümenize bağlanabildiğinizi doğrulamak için bir komut satırında aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="21b4d-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="21b4d-119">Aşağıdaki JSON yanıt almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="21b4d-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="21b4d-120">Bu komutta kullanılan parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="21b4d-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="21b4d-121">**-u**: kullanıcı adı ve istek kimliğini doğrulamak için kullanılan parola</span><span class="sxs-lookup"><span data-stu-id="21b4d-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="21b4d-122">**-G**: Bu isteği bir GET isteği olduğunu gösterir</span><span class="sxs-lookup"><span data-stu-id="21b4d-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="21b4d-123">URL'nin başına **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, tüm istekler için aynıdır.</span><span class="sxs-lookup"><span data-stu-id="21b4d-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="21b4d-124">Yol **/status**, sunucu için istek WebHCat (Templeton olarak da bilinir) durumuna döndürmek için olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="21b4d-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="21b4d-125">Küme için Pig Latin işi göndermek için aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="21b4d-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="21b4d-126">Bu komutta kullanılan parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="21b4d-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="21b4d-127">**-d**: çünkü `-G` kullanılmaz, istek varsayılan olarak, POST yöntemi.</span><span class="sxs-lookup"><span data-stu-id="21b4d-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="21b4d-128">`-d`istekle birlikte gönderilen veri değerleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="21b4d-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="21b4d-129">**User.Name**: komutu çalıştıran kullanıcının</span><span class="sxs-lookup"><span data-stu-id="21b4d-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="21b4d-130">**yürütme**: yürütmek için Pig Latin deyimleri</span><span class="sxs-lookup"><span data-stu-id="21b4d-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="21b4d-131">**statusdir**: Bu iş için durumu yazılır dizini</span><span class="sxs-lookup"><span data-stu-id="21b4d-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="21b4d-132">Pig Latin deyimlerinde alanları değiştirilir bildirimi `+` karakter Curl ile kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="21b4d-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="21b4d-133">Bu komut, örneğin, iş durumunu denetlemek için kullanılan bir iş kimliği döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="21b4d-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="21b4d-134">İş durumunu denetlemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21b4d-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="21b4d-135">Değiştir `JOBID` önceki adımda döndürülen değer.</span><span class="sxs-lookup"><span data-stu-id="21b4d-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="21b4d-136">Örneğin, dönüş değeri `{"id":"job_1415651640909_0026"}`, ardından `JOBID` olan `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="21b4d-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="21b4d-137">İş tamamlandı durumu varsa, **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="21b4d-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="21b4d-138">Bu Curl istek JavaScript nesne gösterimi (JSON) belge ile iş hakkındaki bilgileri döndürür ve jq yalnızca durum değeri almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21b4d-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <span data-ttu-id="21b4d-139"><a id="results"></a>Sonuçları Görüntüle</span><span class="sxs-lookup"><span data-stu-id="21b4d-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="21b4d-140">İş durumunu değiştiği için **başarılı**, iş sonuçları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21b4d-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="21b4d-141">`statusdir` Sorguyla geçirilen parametre içeren çıkış dosyasının; bu durumda, konumu `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="21b4d-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="21b4d-142">Hdınsight Azure Storage veya Azure Data Lake Store varsayılan veri deposu olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21b4d-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="21b4d-143">Hangisinin bağlı olarak, kullandığınız veri almanın çeşitli yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="21b4d-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="21b4d-144">Daha fazla bilgi için depolama bölümüne bakın [Linux tabanlı Hdınsight bilgi](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) belge.</span><span class="sxs-lookup"><span data-stu-id="21b4d-144">For more information, see the storage section of the [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="21b4d-145"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="21b4d-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="21b4d-146">Bu belgede gösterildiği gibi çalıştırın, izlemek ve Hdınsight kümenize Pig işleri sonuçlarını görüntülemek için ham bir HTTP isteği'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21b4d-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="21b4d-147">Bu makalede kullanılan REST arabirimi hakkında daha fazla bilgi için bkz: [WebHCat başvuru](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="21b4d-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="21b4d-148"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21b4d-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="21b4d-149">Hdınsight Pig hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="21b4d-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="21b4d-150">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="21b4d-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="21b4d-151">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21b4d-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="21b4d-152">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="21b4d-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="21b4d-153">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="21b4d-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
