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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Linux tabanlı Hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümleme

Ardından Linux tabanlı Hdınsight'ta Hive kullanma tooanalyze uçuş gecikme veri hello veri tooAzure SQL veritabanı nasıl dışarı öğrenin Sqoop kullanma.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="prerequisites"></a>Ön koşullar

* **Hdınsight kümesi**. Bkz: [Hadoop ile Linux'ta Hdınsight Hive kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md) yeni bir Linux tabanlı Hdınsight kümesi oluşturma adımları için.

* **Azure SQL Veritabanı**. Hedef veri deposu olarak Azure SQL veritabanını kullanın. Bir SQL veritabanı zaten yoksa bkz [SQL Database Öğreticisi: dakika içinde bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md).

* **Azure CLI**. Hello Azure CLI yüklü değilse bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) daha fazla adım için.

## <a name="download-hello-flight-data"></a>Merhaba uçuş veri indirin

1. Çok Gözat[araştırma ve yenilikçi teknoloji yönetim, taşıma İstatistik Enstitüsü][rita-website].

2. Başlangıç sayfasında, aşağıdaki değerleri hello seçin:

   | Ad | Değer |
   | --- | --- |
   | Filtre yıl |2013 |
   | Dönem filtre |Ocak |
   | Alanları |Yıl, FlightDate, UniqueCarrier, taşıyıcı, FlightNum, OriginAirportID, kaynak, OriginCityName, OriginState, DestAirportID, hedef, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Diğer tüm alanlar temizleyin |

3. **İndir**’e tıklayın.

## <a name="upload-hello-data"></a>Merhaba veri yükleme

1. Komut tooupload hello zip dosyası toohello Hdınsight küme baş düğümüne aşağıdaki hello kullan:

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Değiştir **FILENAME** hello zip dosyası hello adı. Değiştir **kullanıcıadı** hello SSH oturum hello Hdınsight kümesi için. CLUSTERNAME hello hello Hdınsight küme adıyla değiştirin.

   > [!NOTE]
   > SSH oturum açma parolası tooauthenticate kullanırsanız, hello parolası istenir. Bir ortak anahtar kullandıysanız, toouse hello gerekebilir `-i` parametre ve özel anahtarı eşleşen hello yolu toohello belirtin. Örneğin, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Merhaba karşıya yükleme tamamlandıktan sonra SSH kullanarak toohello kümesine bağlanın:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Bağlantı kurulduktan sonra aşağıdaki toounzip hello .zip dosyasına hello kullan:

    ```
    unzip FILENAME.zip
    ```

    Bu komut, kabaca 60 MB boyutunda bir .csv dosyası ayıklar.

4. Komut toocreate bir dizin Hdınsight depolama alanında aşağıdaki hello kullanın ve ardından hello dosya toohello dizin kopyalayın:

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>Oluşturma ve hello HiveQL çalıştırma

Kullanım hello aşağıdaki adımları tooimport veri hello CSV dosyasından adlı bir Hive tabloya **gecikmeler**.

1. Kullanım hello aşağıdaki komut toocreate ve adlı yeni bir dosya düzenleme **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:

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

2. toosave hello dosya, kullanım **Ctrl + X**, ardından **Y** .

3. toostart Hive ve çalışma hello **flightdelays.hql** dosya, hello aşağıdaki komutu kullanın:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > Bu örnekte, `localhost` HiveServer2 çalıştığı olduğu hello Hdınsight kümesi baş düğümüne bağlanan toohello olduğundan kullanılır.

4. Bir kez hello __flightdelays.hql__ çalıştıran sonlandığında kullanım hello şu komutu tooopen etkileşimli Beeline oturum bir komut dosyası:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Merhaba aldığınızda `jdbc:hive2://localhost:10001/>` isteminde, sorgu tooretrieve veri içe hello uçuş gecikme verileri aşağıdaki hello kullanın.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    Bu sorgu hello ortalama birlikte deneyimli hava durumu gecikmeler gecikme süresi ve çok kaydedin Şehir listesini alır`/tutorials/flightdelays/output`. Daha sonra Sqoop bu konumdan hello veri okuyan ve tooAzure SQL veritabanı verin.

6. tooexit Beeline, girin `!quit` hello isteminde.

## <a name="create-a-sql-database"></a>SQL Veritabanı oluşturma

Bir SQL veritabanı zaten varsa, hello sunucu adını edinmeniz gerekir. Hello hello sunucu adı bulabilirsiniz [Azure portal](https://portal.azure.com) seçerek **SQL veritabanları**, ve veritabanı hello hello adını filtreleme toouse istiyor. Merhaba sunucu adı hello listelenen **SERVER** sütun.

Bir SQL veritabanı zaten yoksa, hello bilgileri kullanın [SQL Database Öğreticisi: dakika içinde bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md) toocreate biri. Merhaba veritabanı için kullanılan hello sunucu adını kaydedin.

## <a name="create-a-sql-database-table"></a>SQL veritabanı tablosu oluşturma

> [!NOTE]
> Birçok yolu tooconnect tooSQL veritabanı vardır ve bir tablo oluşturun. Aşağıdaki adımları kullan hello [ücretsiz](http://www.freetds.org/) hello Hdınsight kümesine ait.


1. SSH tooconnect toohello Linux tabanlı Hdınsight kümesi ve aşağıdaki adımları hello SSH oturumundan çalışma hello kullanın.

2. Aşağıdaki komut tooinstall ücretsiz hello kullan:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Merhaba yükleme işlemi tamamlandıktan sonra komut tooconnect toohello SQL veritabanı sunucusu aşağıdaki hello kullanın. Değiştir **serverName** hello SQL veritabanı sunucusu adı ile. Değiştir **adminLogin** ve **Admınpassword** hello oturum SQL veritabanı için. Değiştir **databaseName** hello veritabanı adında.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Metin aşağıdaki çıktı benzer toohello alırsınız:

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. Merhaba, `1>` isteminde, aşağıdaki satırları hello girin:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Ne zaman hello `GO` deyimi girilir, hello önceki deyimleri değerlendirilir. Bu sorgu adlı bir tablo oluşturur **gecikmeler**, kümelenmiş bir dizin ile.

    Tablo hello sorgu tooverify aşağıdaki kullanım hello oluşturuldu:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Merhaba, benzer toohello metin aşağıdaki çıktı:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Girin `exit` hello adresindeki `1>` sor tooexit hello tsql yardımcı programı.

## <a name="export-data-with-sqoop"></a>Sqoop ile verileri dışarı aktarma

1. Sqoop SQL veritabanınız görebilirsiniz komutu tooverify aşağıdaki hello kullan:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    Bu komut, veritabanları, daha önce oluşturduğunuz hello gecikmeler tabloda hello veritabanı dahil olmak üzere listesini döndürür.

2. Komut tooexport veri hivesampletable toohello mobiledata tablosundan aşağıdaki hello kullan:

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop hello gecikmeler tablo içeren toohello veritabanına bağlanır ve hello veri aktarır `/tutorials/flightdelays/output` directory toohello gecikmeler tablo.

3. Merhaba komutu tamamlandıktan sonra TSQL kullanarak tooconnect toohello veritabanı aşağıdaki hello kullan:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Bağlantı kurulduktan sonra hello verileri dışarı aktarılan toohello mobiledata tablo olduğunu deyimleri tooverify aşağıdaki hello kullanın:

    ```
    SELECT * FROM delays
    GO
    ```

    Merhaba tablodaki verileri listesini görmelisiniz. Tür `exit` tooexit hello tsql yardımcı programı.

## <a id="nextsteps"></a> Sonraki adımlar

Hdınsight, verilerle daha fazla yol toowork toolearn bkz hello belgeler:

* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [Oozie Hdınsight ile kullanma][hdinsight-use-oozie]
* [Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]
* [Hdınsight için Java MapReduce programlar geliştirmek][hdinsight-develop-mapreduce]
* [Python Hadoop programları Hdınsight için akış geliştirin][hdinsight-develop-streaming]

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
