---
title: "Curl hdınsight'ta - Azure ile Hadoop Hive kullanma | Microsoft Docs"
description: "Curl kullanarak hdınsight'a Pig işleri uzaktan göndermek öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8a4f217b046121f85be0585eab18d90c44f21b9e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="34b5b-103">REST kullanarak hdınsight'ta Hadoop ile Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="34b5b-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="34b5b-104">Azure Hdınsight kümesinde Hadoop ile Hive sorguları çalıştırmak için WebHCat REST API kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="34b5b-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="34b5b-105">[Curl](http://curl.haxx.se/) ham HTTP isteklerini kullanarak Hdınsight ile nasıl etkileşim kurabileceğine göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="34b5b-106">[Jq](http://stedolan.github.io/jq/) yardımcı programı, REST isteklerinden döndürülen JSON verileri işlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="34b5b-107">Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni Hdınsight için, bkz: [Linux tabanlı hdınsight'ta Hadoop hakkında bilmeniz gerekenleri](hdinsight-hadoop-linux-information.md) belge.</span><span class="sxs-lookup"><span data-stu-id="34b5b-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="34b5b-108"><a id="curl"></a>Hive sorgularını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="34b5b-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="34b5b-109">WebHCat ile cURL veya başka bir REST iletişimini kullanırken Hdınsight küme yöneticisinin kullanıcı adını ve parolasını sağlayarak isteklerin kimliğini doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34b5b-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="34b5b-110">Bu bölümdeki komutlar için **USERNAME** ifadesini küme kimliğini doğrulayacak kullanıcı ile, **PASSWORD** ifadesini ise kullanıcı hesabının parolası ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34b5b-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="34b5b-111">**CLUSTERNAME** değerini kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34b5b-111">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="34b5b-112">REST API’sinin güvenliği [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication) ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="34b5b-113">Kimlik bilgilerinizin sunucuya güvenli bir şekilde gönderilir sağlamaya yardımcı olmak için her zaman güvenli HTTP (HTTPS) kullanarak istekleri yapın.</span><span class="sxs-lookup"><span data-stu-id="34b5b-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="34b5b-114">HDInsight kümenize bağlanabildiğinizi doğrulamak için bir komut satırında aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="34b5b-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="34b5b-115">Aşağıdakine benzer bir yanıt alırsınız:</span><span class="sxs-lookup"><span data-stu-id="34b5b-115">You receive a response similar to the following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="34b5b-116">Bu komutta kullanılan parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="34b5b-116">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="34b5b-117">**-u** - İstek kimliğini doğrulamak için kullanılan kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="34b5b-117">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="34b5b-118">**-G** -bu isteği alma işlemi olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="34b5b-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="34b5b-119">URL'nin başına **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, tüm istekler için aynıdır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="34b5b-120">Yol **/status**, sunucu için istek WebHCat (Templeton olarak da bilinir) durumuna döndürmek için olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="34b5b-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="34b5b-121">Ayrıca, aşağıdaki komutu kullanarak Hive sürümü isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34b5b-121">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="34b5b-122">Bu istek aşağıdaki metni benzer bir yanıt döndürür:</span><span class="sxs-lookup"><span data-stu-id="34b5b-122">This request returns a response similar to the following text:</span></span>

       <span data-ttu-id="34b5b-123">{"modülünde": "hive", "Sürüm": "0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="34b5b-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="34b5b-124">Adlı bir tablo oluşturmak için aşağıdakileri kullanın **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="34b5b-124">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="34b5b-125">Bu istekle kullanılan aşağıdaki Parametreler:</span><span class="sxs-lookup"><span data-stu-id="34b5b-125">The following parameters used with this request:</span></span>

   * <span data-ttu-id="34b5b-126">**-d** - bu yana `-G` kullanılmaz, istek varsayılan olarak, POST yöntemi.</span><span class="sxs-lookup"><span data-stu-id="34b5b-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="34b5b-127">`-d`istekle birlikte gönderilen veri değerleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="34b5b-127">`-d` specifies the data values that are sent with the request.</span></span>

     * <span data-ttu-id="34b5b-128">**User.Name** -komutu çalıştıran kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="34b5b-128">**user.name** - The user that is running the command.</span></span>
     * <span data-ttu-id="34b5b-129">**yürütme** -HiveQL ifadelerini yürütülecek.</span><span class="sxs-lookup"><span data-stu-id="34b5b-129">**execute** - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="34b5b-130">**statusdir** -bu iş için durumu yazılır dizin.</span><span class="sxs-lookup"><span data-stu-id="34b5b-130">**statusdir** - The directory that the status for this job is written to.</span></span>

     <span data-ttu-id="34b5b-131">Bu ifadeler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="34b5b-131">These statements perform the following actions:</span></span>
   * <span data-ttu-id="34b5b-132">**DROP TABLE** -tablosu zaten silinmiş.</span><span class="sxs-lookup"><span data-stu-id="34b5b-132">**DROP TABLE** - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="34b5b-133">**Dış tablo oluştur** -kovanında yeni bir 'external' tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34b5b-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="34b5b-134">Dış tablolara yalnızca tablo tanımı kovanında depolar.</span><span class="sxs-lookup"><span data-stu-id="34b5b-134">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="34b5b-135">Veriler özgün konumda kalır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-135">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="34b5b-136">Dış kaynak tarafından güncelleştirilecek temel alınan veri beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-136">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="34b5b-137">Örneğin, bir otomatik veri karşıya yükleme işlemi veya başka bir MapReduce işlemi.</span><span class="sxs-lookup"><span data-stu-id="34b5b-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="34b5b-138">Bir dış tablo bırakma mu **değil** verileri, yalnızca tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="34b5b-138">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="34b5b-139">**SATIR biçimi** - verileri biçimlendirilmiş nasıl.</span><span class="sxs-lookup"><span data-stu-id="34b5b-139">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="34b5b-140">Her günlüğüne alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-140">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="34b5b-141">**AS TEXTFILE konumu DEPOLANAN** - verilerinin depolandığı (örneğin/veri dizini) ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="34b5b-142">**SEÇİN** -tüm satırların sayımını seçer Burada sütun **t4** değeri içeren **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="34b5b-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="34b5b-143">Bu ifade değerini döndürür **3** bu değeri içeren üç satır olarak.</span><span class="sxs-lookup"><span data-stu-id="34b5b-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="34b5b-144">HiveQL ifadelerini arasında boşluk değiştirilir bildirimi `+` karakter Curl ile kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="34b5b-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="34b5b-145">Sınırlayıcı gibi bir alanı içeren tırnak içine alınmış değerler değiştirilmemişse tarafından `+`.</span><span class="sxs-lookup"><span data-stu-id="34b5b-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="34b5b-146">**'% 25.log' INPUT__FILE__NAME gibi** -bu deyim yalnızca biten dosyaları kullanmak üzere aramayı sınırlar. günlük.</span><span class="sxs-lookup"><span data-stu-id="34b5b-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="34b5b-147">`%25` Gerçek koşul %, URL kodlanmış form olduğundan `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="34b5b-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span></span> <span data-ttu-id="34b5b-148">% URL'lerde özel karakter olarak değerlendirildiğinden URL kodlanmış, olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34b5b-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="34b5b-149">Bu komut, iş durumunu denetlemek için kullanılan bir iş kimliği döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="34b5b-149">This command should return a job ID that can be used to check the status of the job.</span></span>

       <span data-ttu-id="34b5b-150">{"ID": "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="34b5b-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="34b5b-151">İş durumunu denetlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="34b5b-151">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="34b5b-152">Değiştir **JOBID** önceki adımda döndürülen değer.</span><span class="sxs-lookup"><span data-stu-id="34b5b-152">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="34b5b-153">Örneğin, dönüş değeri `{"id":"job_1415651640909_0026"}`, ardından **JOBID** olacaktır `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="34b5b-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="34b5b-154">İş tamamlandı durumu varsa, **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="34b5b-154">If the job has finished, the state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="34b5b-155">Bu Curl istek JavaScript nesne gösterimi (JSON) belge ile iş hakkındaki bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="34b5b-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span></span> <span data-ttu-id="34b5b-156">Jq yalnızca durum değeri almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34b5b-156">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="34b5b-157">İş durumu olarak değiştirildi sonra **başarılı**, Azure Blob depolama alanından iş sonuçlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34b5b-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="34b5b-158">`statusdir` Sorguyla geçirilen parametre içeren çıkış dosyasının; bu durumda, konumu **/örnek/curl**.</span><span class="sxs-lookup"><span data-stu-id="34b5b-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="34b5b-159">Bu adres çıktıda depolar **örnek/curl** kümeleri varsayılan depolama birimindeki dizin.</span><span class="sxs-lookup"><span data-stu-id="34b5b-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span></span>

    <span data-ttu-id="34b5b-160">Liste ve kullanarak bu dosyaları indirmek [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="34b5b-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="34b5b-161">Azure Storage ile Azure CLI kullanma ile ilgili daha fazla bilgi için bkz: [Azure Storage ile Azure CLI 2.0 Kullan](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) belge.</span><span class="sxs-lookup"><span data-stu-id="34b5b-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="34b5b-162">Adlı yeni bir 'iç' tablo oluşturmak için aşağıdaki deyimleri kullanın **günlüklerini**:</span><span class="sxs-lookup"><span data-stu-id="34b5b-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="34b5b-163">Bu ifadeler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="34b5b-163">These statements perform the following actions:</span></span>

   * <span data-ttu-id="34b5b-164">**Tablo IF değil var oluşturmak** -zaten yoksa, bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34b5b-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="34b5b-165">Bu bildirimi Hive veri ambarında depolanır ve Hive tamamen yönetilen bir iç bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34b5b-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="34b5b-166">Dış tablolara, bir iç tablosu bırakarak temel alınan veri de siler.</span><span class="sxs-lookup"><span data-stu-id="34b5b-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="34b5b-167">**AS ORC DEPOLANAN** -en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="34b5b-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="34b5b-168">ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="34b5b-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="34b5b-169">**INSERT ÜZERİNE... SEÇİN** -satırları seçer **log4jLogs** içeren tablo **[Hata]**, verileri ekler **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="34b5b-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>
   * <span data-ttu-id="34b5b-170">**SEÇİN** -tüm satırları yeni seçer **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="34b5b-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span></span>

6. <span data-ttu-id="34b5b-171">İş durumunu denetlemek için döndürülen iş Kimliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="34b5b-171">Use the job ID returned to check the status of the job.</span></span> <span data-ttu-id="34b5b-172">Başarılı olduktan sonra Azure CLI açıklandığı gibi önceden indirmek ve sonuçları görüntülemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="34b5b-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span></span> <span data-ttu-id="34b5b-173">Çıktı da içeren üç satırları içermelidir **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="34b5b-173">The output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="34b5b-174"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34b5b-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="34b5b-175">Hdınsight ile Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="34b5b-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="34b5b-176">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="34b5b-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="34b5b-177">Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34b5b-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="34b5b-178">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="34b5b-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="34b5b-179">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="34b5b-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="34b5b-180">Tez Hive ile kullanıyorsanız, hata ayıklama bilgileri için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="34b5b-180">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="34b5b-181">Linux tabanlı Hdınsight üzerinde Ambari Tez görünümünü kullanın</span><span class="sxs-lookup"><span data-stu-id="34b5b-181">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="34b5b-182">Bu belgede kullanılan REST API hakkında daha fazla bilgi için bkz: [WebHCat başvuru](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) belge.</span><span class="sxs-lookup"><span data-stu-id="34b5b-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


