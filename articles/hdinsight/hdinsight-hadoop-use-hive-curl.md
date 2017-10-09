---
title: "aaaUse Curl hdınsight'ta - Azure ile Hadoop Hive | Microsoft Docs"
description: "Curl kullanarak tooHDInsight nasıl tooremotely gönderme Pig işleri öğrenin."
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
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="4332e-103">REST kullanarak hdınsight'ta Hadoop ile Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4332e-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="4332e-104">Toouse hello WebHCat REST API toorun Hive Hadoop ile Azure Hdınsight kümesinde nasıl sorgular öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4332e-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="4332e-105">[Curl](http://curl.haxx.se/) nasıl, etkileşimli olarak çalışabilir Hdınsight ile ham HTTP isteklerini kullanarak kullanılan toodemonstrate değil.</span><span class="sxs-lookup"><span data-stu-id="4332e-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="4332e-106">Merhaba [jq](http://stedolan.github.io/jq/) programıdır kullanılan tooprocess hello JSON verilerini REST isteklerinden döndürdü.</span><span class="sxs-lookup"><span data-stu-id="4332e-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="4332e-107">Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni tooHDInsight hello bkz [gerekenleri Linux tabanlı hdınsight'ta Hadoop hakkında tooknow](hdinsight-hadoop-linux-information.md) belge.</span><span class="sxs-lookup"><span data-stu-id="4332e-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="4332e-108"><a id="curl"></a>Hive sorgularını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4332e-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="4332e-109">Curl'ü veya başka bir REST iletişimini WebHCat ile kullanırken, hello kullanıcı adı ve parola hello Hdınsight küme yöneticisinin sağlayarak hello istekleri kimliğini doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4332e-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="4332e-110">Bu bölümdeki Hello komutlar için Değiştir **kullanıcıadı** hello kullanıcı tooauthenticate toohello küme ve Değiştir **parola** hello hello kullanıcı hesabının parolasını ile.</span><span class="sxs-lookup"><span data-stu-id="4332e-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="4332e-111">Değiştir **CLUSTERNAME** kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="4332e-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="4332e-112">Merhaba REST API aracılığıyla güvenli [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="4332e-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="4332e-113">toohelp kimlik bilgilerinizi güvenli olduğundan emin olun toohello sunucu gönderilen, her zaman güvenli HTTP (HTTPS) kullanarak isteklerde.</span><span class="sxs-lookup"><span data-stu-id="4332e-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="4332e-114">Bir komut satırından tooyour Hdınsight kümesi bağlanabilir komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="4332e-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="4332e-115">Metin izleyen bir yanıt benzer toohello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="4332e-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="4332e-116">Bu komutta kullanılan hello parametreler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4332e-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="4332e-117">**-u** -hello kullanıcı adı ve parola kullanılan tooauthenticate hello isteği.</span><span class="sxs-lookup"><span data-stu-id="4332e-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="4332e-118">**-G** -bu isteği alma işlemi olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4332e-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="4332e-119">Merhaba URL'sini başlayan hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, olan hello aynı tüm istekler için.</span><span class="sxs-lookup"><span data-stu-id="4332e-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="4332e-120">Merhaba yolu **/status**, o hello isteği tooreturn WebHCat (Templeton olarak da bilinir) durumunu hello sunucusu için gösterir.</span><span class="sxs-lookup"><span data-stu-id="4332e-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="4332e-121">Hive hello sürümü komutu aşağıdaki hello kullanarak da isteğinde bulunabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4332e-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="4332e-122">Bu istek metnini izleyen bir yanıt benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="4332e-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="4332e-123">{"modülünde": "hive", "Sürüm": "0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="4332e-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="4332e-124">Toocreate adlı bir tablo aşağıdaki kullanım hello **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="4332e-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="4332e-125">Bu istekle kullanılan parametreler aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="4332e-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="4332e-126">**-d** - bu yana `-G` kullanılmaz, hello isteği varsayılan olarak toohello POST yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4332e-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="4332e-127">`-d`gönderilen Merhaba veri değerleri ile Merhaba isteğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4332e-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="4332e-128">**User.Name** -hello komutu çalıştıran hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="4332e-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="4332e-129">**yürütme** -HiveQL ifadelerini tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="4332e-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="4332e-130">**statusdir** -bu iş için durumu hello hello dizin yazılır.</span><span class="sxs-lookup"><span data-stu-id="4332e-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="4332e-131">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4332e-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="4332e-132">**DROP TABLE** -hello tablo zaten silinmiş.</span><span class="sxs-lookup"><span data-stu-id="4332e-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="4332e-133">**Dış tablo oluştur** -kovanında yeni bir 'external' tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4332e-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="4332e-134">Dış tablolara yalnızca hello tablo tanımı kovanında depolar.</span><span class="sxs-lookup"><span data-stu-id="4332e-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="4332e-135">Merhaba veri hello özgün konumda kalır.</span><span class="sxs-lookup"><span data-stu-id="4332e-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4332e-136">Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4332e-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="4332e-137">Örneğin, bir otomatik veri karşıya yükleme işlemi veya başka bir MapReduce işlemi.</span><span class="sxs-lookup"><span data-stu-id="4332e-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="4332e-138">Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.</span><span class="sxs-lookup"><span data-stu-id="4332e-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="4332e-139">**SATIR biçimi** - hello veri biçimlendirilmiş nasıl.</span><span class="sxs-lookup"><span data-stu-id="4332e-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="4332e-140">Her günlüğüne Hello alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="4332e-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="4332e-141">**AS TEXTFILE konumu DEPOLANAN** - hello veriler burada (Merhaba örnek/veri dizini) ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="4332e-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="4332e-142">**SEÇİN** -tüm satırların sayımını seçer Burada sütun **t4** hello değeri içeren **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="4332e-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="4332e-143">Bu ifade değerini döndürür **3** bu değeri içeren üç satır olarak.</span><span class="sxs-lookup"><span data-stu-id="4332e-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4332e-144">Merhaba alanları HiveQL ifadelerini arasında hello tarafından değiştirilir fark `+` karakter Curl ile kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="4332e-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="4332e-145">Merhaba sınırlayıcı gibi bir alanı içeren tırnak içine alınmış değerler değiştirilmemişse tarafından `+`.</span><span class="sxs-lookup"><span data-stu-id="4332e-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="4332e-146">**'% 25.log' INPUT__FILE__NAME gibi** - biten bu deyimi sınırları hello arama tooonly dosyaları kullanma. günlük.</span><span class="sxs-lookup"><span data-stu-id="4332e-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4332e-147">Merhaba `%25` hello gerçek koşul hello URL kodlanmış form %, olduğundan `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="4332e-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="4332e-148">Merhaba % toobe URL kodlanmış, aynıdır URL'lerde özel karakter olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="4332e-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="4332e-149">Bu komut, kullanılan toocheck hello hello işinin durumunu olabilir bir iş kimliği döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="4332e-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="4332e-150">{"ID": "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="4332e-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="4332e-151">Merhaba işinin komutu aşağıdaki kullanım hello toocheck hello durumu:</span><span class="sxs-lookup"><span data-stu-id="4332e-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="4332e-152">Değiştir **JOBID** hello önceki adımda döndürülen hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="4332e-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="4332e-153">Örneğin, hello değeri döndürür `{"id":"job_1415651640909_0026"}`, ardından **JOBID** olacaktır `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="4332e-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="4332e-154">Merhaba işi tamamlanmadan hello durumu varsa, **başarılı**.</span><span class="sxs-lookup"><span data-stu-id="4332e-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4332e-155">Bu Curl istek JavaScript nesne gösterimi (JSON) belge hello işi hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="4332e-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="4332e-156">Jq kullanılan tooretrieve yalnızca hello durum değeri.</span><span class="sxs-lookup"><span data-stu-id="4332e-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="4332e-157">Merhaba işin Hello durumu çok değişti sonra**başarılı**, Azure Blob depolama alanından hello iş hello sonuçlarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4332e-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="4332e-158">Merhaba `statusdir` hello sorguyla geçirilen parametre içeren hello çıkış dosyasının; bu durumda, hello konumu **/örnek/curl**.</span><span class="sxs-lookup"><span data-stu-id="4332e-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="4332e-159">Bu adres hello çıktı hello depolar **örnek/curl** hello dizininde kümeleri varsayılan depolama.</span><span class="sxs-lookup"><span data-stu-id="4332e-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="4332e-160">Liste ve hello kullanarak bu dosyaları indirmek [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4332e-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="4332e-161">Merhaba hello Azure CLI Azure Storage ile kullanma hakkında daha fazla bilgi için bkz: [Azure Storage ile Azure CLI 2.0 Kullan](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) belge.</span><span class="sxs-lookup"><span data-stu-id="4332e-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="4332e-162">Aşağıdaki deyimleri toocreate adlı yeni bir 'iç' tablo kullanım hello **günlüklerini**:</span><span class="sxs-lookup"><span data-stu-id="4332e-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="4332e-163">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4332e-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="4332e-164">**Tablo IF değil var oluşturmak** -zaten yoksa, bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4332e-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="4332e-165">Bu bildirimi hello Hive veri ambarında depolanır ve Hive tamamen yönetilen bir iç bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4332e-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4332e-166">Dış tablolara, bir iç tablosu bırakarak hello temel alınan veri de siler.</span><span class="sxs-lookup"><span data-stu-id="4332e-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="4332e-167">**AS ORC DEPOLANAN** -en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde hello verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="4332e-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="4332e-168">ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="4332e-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="4332e-169">**INSERT ÜZERİNE... SEÇİN** -hello satırları seçer **log4jLogs** içeren tablo **[Hata]**, eklemeleri veri hello hello sonra **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="4332e-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="4332e-170">**SEÇİN** -hello yeni tüm satırları seçer **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="4332e-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="4332e-171">Kullanım hello iş kimliği toocheck hello hello işinin durumunu döndürdü.</span><span class="sxs-lookup"><span data-stu-id="4332e-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="4332e-172">Başarılı olduktan sonra hello toodownload ve görünüm hello sonuçları daha önce açıklandığı gibi Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="4332e-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="4332e-173">Merhaba çıktı, her biri içeren üç satırları içermelidir **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="4332e-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="4332e-174"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4332e-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="4332e-175">Hdınsight ile Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="4332e-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="4332e-176">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="4332e-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="4332e-177">Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4332e-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="4332e-178">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="4332e-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="4332e-179">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="4332e-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="4332e-180">Tez Hive ile kullanıyorsanız, belgeleri hata ayıklama bilgileri için aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="4332e-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="4332e-181">Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın</span><span class="sxs-lookup"><span data-stu-id="4332e-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="4332e-182">Merhaba hello bu belgede kullanılan REST API hakkında daha fazla bilgi için bkz: [WebHCat başvuru](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) belge.</span><span class="sxs-lookup"><span data-stu-id="4332e-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


