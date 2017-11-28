---
title: "hdınsight'ta - Azure Hive aaaAnalyze uçuş gecikme verilerle | Microsoft Docs"
description: "Nasıl toouse tooanalyze uçuş veri Linux tabanlı hdınsight'ta Hive ve ardından hello veri tooSQL verme öğrenin Sqoop kullanarak veritabanı."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="f9aa5-103">Linux tabanlı Hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="f9aa5-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="f9aa5-104">Ardından Linux tabanlı Hdınsight'ta Hive kullanma tooanalyze uçuş gecikme veri hello veri tooAzure SQL veritabanı nasıl dışarı öğrenin Sqoop kullanma.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9aa5-105">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="f9aa5-106">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f9aa5-107">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f9aa5-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f9aa5-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f9aa5-108">Prerequisites</span></span>

* <span data-ttu-id="f9aa5-109">**Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="f9aa5-110">Bkz: [Hadoop ile Linux'ta Hdınsight Hive kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md) yeni bir Linux tabanlı Hdınsight kümesi oluşturma adımları için.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="f9aa5-111">**Azure SQL Veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-111">**Azure SQL Database**.</span></span> <span data-ttu-id="f9aa5-112">Hedef veri deposu olarak Azure SQL veritabanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="f9aa5-113">Bir SQL veritabanı zaten yoksa bkz [SQL Database Öğreticisi: dakika içinde bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f9aa5-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="f9aa5-114">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-114">**Azure CLI**.</span></span> <span data-ttu-id="f9aa5-115">Hello Azure CLI yüklü değilse bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) daha fazla adım için.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="f9aa5-116">Merhaba uçuş veri indirin</span><span class="sxs-lookup"><span data-stu-id="f9aa5-116">Download hello flight data</span></span>

1. <span data-ttu-id="f9aa5-117">Çok Gözat[araştırma ve yenilikçi teknoloji yönetim, taşıma İstatistik Enstitüsü][rita-website].</span><span class="sxs-lookup"><span data-stu-id="f9aa5-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="f9aa5-118">Başlangıç sayfasında, aşağıdaki değerleri hello seçin:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="f9aa5-119">Ad</span><span class="sxs-lookup"><span data-stu-id="f9aa5-119">Name</span></span> | <span data-ttu-id="f9aa5-120">Değer</span><span class="sxs-lookup"><span data-stu-id="f9aa5-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="f9aa5-121">Filtre yıl</span><span class="sxs-lookup"><span data-stu-id="f9aa5-121">Filter Year</span></span> |<span data-ttu-id="f9aa5-122">2013</span><span class="sxs-lookup"><span data-stu-id="f9aa5-122">2013</span></span> |
   | <span data-ttu-id="f9aa5-123">Dönem filtre</span><span class="sxs-lookup"><span data-stu-id="f9aa5-123">Filter Period</span></span> |<span data-ttu-id="f9aa5-124">Ocak</span><span class="sxs-lookup"><span data-stu-id="f9aa5-124">January</span></span> |
   | <span data-ttu-id="f9aa5-125">Alanları</span><span class="sxs-lookup"><span data-stu-id="f9aa5-125">Fields</span></span> |<span data-ttu-id="f9aa5-126">Yıl, FlightDate, UniqueCarrier, taşıyıcı, FlightNum, OriginAirportID, kaynak, OriginCityName, OriginState, DestAirportID, hedef, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="f9aa5-127">Diğer tüm alanlar temizleyin</span><span class="sxs-lookup"><span data-stu-id="f9aa5-127">Clear all other fields</span></span> |

3. <span data-ttu-id="f9aa5-128">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="f9aa5-129">Merhaba veri yükleme</span><span class="sxs-lookup"><span data-stu-id="f9aa5-129">Upload hello data</span></span>

1. <span data-ttu-id="f9aa5-130">Komut tooupload hello zip dosyası toohello Hdınsight küme baş düğümüne aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="f9aa5-131">Değiştir **FILENAME** hello zip dosyası hello adı.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="f9aa5-132">Değiştir **kullanıcıadı** hello SSH oturum hello Hdınsight kümesi için.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="f9aa5-133">CLUSTERNAME hello hello Hdınsight küme adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f9aa5-134">SSH oturum açma parolası tooauthenticate kullanırsanız, hello parolası istenir.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="f9aa5-135">Bir ortak anahtar kullandıysanız, toouse hello gerekebilir `-i` parametre ve özel anahtarı eşleşen hello yolu toohello belirtin.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="f9aa5-136">Örneğin, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="f9aa5-137">Merhaba karşıya yükleme tamamlandıktan sonra SSH kullanarak toohello kümesine bağlanın:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="f9aa5-138">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f9aa5-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="f9aa5-139">Bağlantı kurulduktan sonra aşağıdaki toounzip hello .zip dosyasına hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="f9aa5-140">Bu komut, kabaca 60 MB boyutunda bir .csv dosyası ayıklar.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="f9aa5-141">Komut toocreate bir dizin Hdınsight depolama alanında aşağıdaki hello kullanın ve ardından hello dosya toohello dizin kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="f9aa5-142">Oluşturma ve hello HiveQL çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f9aa5-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="f9aa5-143">Kullanım hello aşağıdaki adımları tooimport veri hello CSV dosyasından adlı bir Hive tabloya **gecikmeler**.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="f9aa5-144">Kullanım hello aşağıdaki komut toocreate ve adlı yeni bir dosya düzenleme **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="f9aa5-145">Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-145">Use hello following text as hello contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. <span data-ttu-id="f9aa5-146">toosave hello dosya, kullanım **Ctrl + X**, ardından **Y** .</span><span class="sxs-lookup"><span data-stu-id="f9aa5-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="f9aa5-147">toostart Hive ve çalışma hello **flightdelays.hql** dosya, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="f9aa5-148">Bu örnekte, `localhost` HiveServer2 çalıştığı olduğu hello Hdınsight kümesi baş düğümüne bağlanan toohello olduğundan kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="f9aa5-149">Bir kez hello __flightdelays.hql__ çalıştıran sonlandığında kullanım hello şu komutu tooopen etkileşimli Beeline oturum bir komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="f9aa5-150">Merhaba aldığınızda `jdbc:hive2://localhost:10001/>` isteminde, sorgu tooretrieve veri içe hello uçuş gecikme verileri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="f9aa5-151">Bu sorgu hello ortalama birlikte deneyimli hava durumu gecikmeler gecikme süresi ve çok kaydedin Şehir listesini alır`/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="f9aa5-152">Daha sonra Sqoop bu konumdan hello veri okuyan ve tooAzure SQL veritabanı verin.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="f9aa5-153">tooexit Beeline, girin `!quit` hello isteminde.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="f9aa5-154">SQL Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9aa5-154">Create a SQL Database</span></span>

<span data-ttu-id="f9aa5-155">Bir SQL veritabanı zaten varsa, hello sunucu adını edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="f9aa5-156">Hello hello sunucu adı bulabilirsiniz [Azure portal](https://portal.azure.com) seçerek **SQL veritabanları**, ve veritabanı hello hello adını filtreleme toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="f9aa5-157">Merhaba sunucu adı hello listelenen **SERVER** sütun.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="f9aa5-158">Bir SQL veritabanı zaten yoksa, hello bilgileri kullanın [SQL Database Öğreticisi: dakika içinde bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md) toocreate biri.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="f9aa5-159">Merhaba veritabanı için kullanılan hello sunucu adını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="f9aa5-160">SQL veritabanı tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9aa5-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="f9aa5-161">Birçok yolu tooconnect tooSQL veritabanı vardır ve bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="f9aa5-162">Aşağıdaki adımları kullan hello [ücretsiz](http://www.freetds.org/) hello Hdınsight kümesine ait.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="f9aa5-163">SSH tooconnect toohello Linux tabanlı Hdınsight kümesi ve aşağıdaki adımları hello SSH oturumundan çalışma hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="f9aa5-164">Aşağıdaki komut tooinstall ücretsiz hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="f9aa5-165">Merhaba yükleme işlemi tamamlandıktan sonra komut tooconnect toohello SQL veritabanı sunucusu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="f9aa5-166">Değiştir **serverName** hello SQL veritabanı sunucusu adı ile.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="f9aa5-167">Değiştir **adminLogin** ve **Admınpassword** hello oturum SQL veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="f9aa5-168">Değiştir **databaseName** hello veritabanı adında.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="f9aa5-169">Metin aşağıdaki çıktı benzer toohello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="f9aa5-170">Merhaba, `1>` isteminde, aşağıdaki satırları hello girin:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="f9aa5-171">Ne zaman hello `GO` deyimi girilir, hello önceki deyimleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="f9aa5-172">Bu sorgu adlı bir tablo oluşturur **gecikmeler**, kümelenmiş bir dizin ile.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="f9aa5-173">Tablo hello sorgu tooverify aşağıdaki kullanım hello oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="f9aa5-174">Merhaba, benzer toohello metin aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="f9aa5-175">Girin `exit` hello adresindeki `1>` sor tooexit hello tsql yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="f9aa5-176">Sqoop ile verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="f9aa5-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="f9aa5-177">Sqoop SQL veritabanınız görebilirsiniz komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="f9aa5-178">Bu komut, veritabanları, daha önce oluşturduğunuz hello gecikmeler tabloda hello veritabanı dahil olmak üzere listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="f9aa5-179">Komut tooexport veri hivesampletable toohello mobiledata tablosundan aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="f9aa5-180">Sqoop hello gecikmeler tablo içeren toohello veritabanına bağlanır ve hello veri aktarır `/tutorials/flightdelays/output` directory toohello gecikmeler tablo.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="f9aa5-181">Merhaba komutu tamamlandıktan sonra TSQL kullanarak tooconnect toohello veritabanı aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="f9aa5-182">Bağlantı kurulduktan sonra hello verileri dışarı aktarılan toohello mobiledata tablo olduğunu deyimleri tooverify aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="f9aa5-183">Merhaba tablodaki verileri listesini görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="f9aa5-184">Tür `exit` tooexit hello tsql yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="f9aa5-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="f9aa5-185"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9aa5-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="f9aa5-186">Hdınsight, verilerle daha fazla yol toowork toolearn bkz hello belgeler:</span><span class="sxs-lookup"><span data-stu-id="f9aa5-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="f9aa5-187">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f9aa5-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f9aa5-188">[Oozie Hdınsight ile kullanma][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="f9aa5-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="f9aa5-189">[Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="f9aa5-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="f9aa5-190">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f9aa5-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f9aa5-191">[Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="f9aa5-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="f9aa5-192">[Python Hadoop programları Hdınsight için akış geliştirin][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="f9aa5-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
