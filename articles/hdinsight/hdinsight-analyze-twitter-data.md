---
title: "Twitter verilerini hdınsight'ta - Azure Hadoop ile aaaAnalyze | Microsoft Docs"
description: "Belirli bir sözcük kullanımı sıklığını toouse Hive tooanalyze Twitter verileri hadoop'ta Hdınsight toofind nasıl hello öğrenin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Twitter verilerini hdınsight'ta Hive kullanma çözümleme
Sosyal Web siteleri hello ana yönlendirmeli zorlar, büyük veri benimseme için biridir. Twitter gibi siteler tarafından sağlanan ortak API'ler verileri çözümlemek ve popüler eğilimleri anlamak için yararlı bir kaynaktır.
Bu öğreticide, API akış Twitter kullanarak tweet'leri alın ve sonra Apache Hive Azure Hdınsight tooget belirli bir sözcük bulunan çoğu tweet'leri hello gönderen Twitter kullanıcıların listesini kullanın.

> [!IMPORTANT]
> Merhaba bu belgedeki adımlar Windows tabanlı Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). Linux tabanlı olan adımları belirli tooa küme için bkz: [(Linux) hdınsight'ta Hive kullanarak Analiz Twitter veri](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir iş istasyonu** Azure yüklenir ve yapılandırılır. PowerShell ile.

    tooexecute Windows PowerShell komut dosyaları, Azure PowerShell'i yönetici olarak çalıştırın ve hello yürütme İlkesi çok ayarlamanız gerekir*RemoteSigned*. Bkz: [çalıştırmak Windows PowerShell komut dosyalarını][powershell-script].

    Windows PowerShell komut dosyalarını çalıştırmadan önce aşağıdaki cmdlet'i hello kullanarak bağlı tooyour Azure aboneliği olduğundan emin olun:

    ```powershell
    Login-AzureRmAccount
    ```

    Birden çok Azure aboneliğiniz varsa, aşağıdaki cmdlet'i tooset hello geçerli abonelik hello kullanın:

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır. Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.
    >
    > Lütfen başlangıç adımları izleyin [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü. Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.

* **Azure Hdınsight kümesi**. Küme sağlama ile ilgili yönergeler için bkz: [Hdınsight kullanmaya başlama] [ hdinsight-get-started] veya [Hdınsight kümeleri hazırlama][hdinsight-provision]. Daha sonra hello öğreticide hello küme adı gerekir.

Merhaba aşağıdaki tabloda Bu öğreticide kullanılan hello dosyaları listeler:

| Dosyalar | Açıklama |
| --- | --- |
| /Tutorials/twitter/Data/tweets.txt |Merhaba Hive işi için kaynak verilerini Hello. |
| /Tutorials/twitter/Output |Merhaba Hive işi için Hello çıkış klasörü. Merhaba varsayılan Hive işi çıkış dosyası adı olan **000000_0**. |
| Tutorials/twitter/twitter.hql |Merhaba HiveQL komut dosyası. |
| /Tutorials/twitter/JobStatus |Merhaba Hadoop iş durumu. |

## <a name="get-twitter-feed"></a>Get Twitter akışı
Bu öğreticide, hello kullanacağı [API'leri akış Twitter][twitter-streaming-api]. Merhaba kullanacağınız API akış belirli Twitter olan [durumları/filtre][twitter-statuses-filter].

> [!NOTE]
> 10.000 tweet'leri ve hello Hive betik dosyası (Merhaba sonraki bölümde yer alan) içeren bir dosyayı yüklediğiniz bir ortak Blob kapsayıcısında. Toouse hello karşıya yüklenen dosyaların istiyorsanız bu bölümü atlayabilirsiniz.

[Tweet'leri veri](https://dev.twitter.com/docs/platform-objects/tweets) karmaşık bir iç içe geçmiş yapısının hello JavaScript nesne gösterimi (JSON) biçiminde depolanır. Böylece bir yapılandırılmış sorgu dili (SQL) tarafından sorgulanabilir geleneksel bir programlama dili kullanarak kod satır sayısını yazmak yerine, iç içe geçmiş bu yapı bir Hive tabloya dönüştürebilirsiniz-HiveQL adında dil ister.

Twitter OAuth yetkili tooprovide erişim tooits API'sini kullanır. OAuth parolalarını paylaşmadan onların adına kullanıcılar tooapprove uygulamaları tooact sağlayan bir kimlik doğrulama protokolüdür. Daha fazla bilgi bulunabilir [oauth.net](http://oauth.net/) veya hello mükemmel [Başlangıç Kılavuzu tooOAuth](http://hueniverse.com/oauth/) Hueniverse gelen.

Merhaba ilk adım toouse OAuth toocreate hello Twitter Developer sitesinde yeni bir uygulama olur.

**toocreate Twitter uygulama**

1. Çok oturum[https://apps.twitter.com/](https://apps.twitter.com/). Merhaba tıklatın **şimdi kaydolun** bir Twitter hesabı yoksa bağlantı.
2. Tıklatın **yeni uygulama oluştur**.
3. Girin **adı**, **açıklama**, **Web sitesi**. Hello için bir URL yukarı yapabileceğiniz **Web sitesi** alan. Aşağıdaki tablonun hello bazı örnek değerleri toouse gösterir:

   | Alan | Değer |
   | --- | --- |
   |  Ad |MyHDInsightApp |
   |  Açıklama |MyHDInsightApp |
   |  Web sitesi |http://www.myhdinsightapp.com |
4. Denetleme **Evet, kabul ediyorum**ve ardından **Twitter uygulamanızı oluşturma**.
5. Merhaba tıklatın **izinleri** sekmesini hello varsayılan izni **salt okunur**. Bu öğretici için yeterli olur.
6. Merhaba tıklatın **anahtarları ve erişim belirteçleri** sekmesi.
7. Tıklatın **my erişim belirteci oluşturma**.
8. Tıklatın **Test OAuth** hello sayfasının hello sağ üst köşesindeki.
9. Yazma **tüketici anahtarı**, **tüketici gizli**, **erişim belirteci**, ve **erişim belirteci gizli anahtarı**. Daha sonra hello öğreticide hello değerleri gerekir.

Bu öğreticide, Windows PowerShell toomake hello web hizmeti çağrısı kullanır. Bir .NET C# örnek için bkz: [hdınsight'ta HBase ile gerçek zamanlı Twitter düşüncelerini çözümleme][hdinsight-hbase-twitter-sentiment]. Merhaba diğer popüler araç toomake web hizmeti çağrıları olan [ *Curl*][curl]. Curl adresinden yüklenebilir [burada][curl-download].

> [!NOTE]
> Windows hello curl komutunu kullandığınızda, çift tırnak işareti yerine tek tırnak hello seçeneği değerleri için kullanın.

**tooget tweet'leri**

1. Merhaba Windows PowerShell Tümleşik komut dosyası ortamı (ISE) açın. (Merhaba Windows 8 Başlat ekranında, yazın **PowerShell_ISE** ve ardından **Windows PowerShell ISE**. Bkz: [başlangıç Windows 8'de Windows PowerShell ve Windows][powershell-start].)
2. Komut dosyası hello betik bölmesine aşağıdaki hello kopyalayın:

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Merhaba ilk beş tooeight değişkenleri hello komut dosyasında ayarlayın:

    Değişken|Açıklama
    ---|---
    $clusterName|Bu hello toorun Merhaba uygulaması istediğiniz hello Hdınsight küme adıdır.
    $oauth_consumer_key|Merhaba Twitter uygulaması budur **tüketici anahtarı** Merhaba Twitter uygulaması oluşturduğunuzda, daha önce yazdığınız.
    $oauth_consumer_secret|Merhaba Twitter uygulaması budur **tüketici gizli** daha önce yazmış.
    $oauth_token|Merhaba Twitter uygulaması budur **erişim belirteci** daha önce yazmış.
    $oauth_token_secret|Merhaba Twitter uygulaması budur **erişim belirteci gizli anahtarı** daha önce yazmış.
    $destBlobName|Merhaba çıkış blob adı budur. Merhaba varsayılan değer **tutorials/twitter/data/tweets.txt**. Merhaba varsayılan değeri değiştirirseniz, tooupdate hello Windows PowerShell komut dosyaları uygun şekilde gerekir.
    $trackString|Merhaba web hizmeti tweet'leri ilgili toothese anahtar sözcükleri döndürür. Merhaba varsayılan değer **Azure, bulut, Hdınsight**. Merhaba varsayılan değeri değiştirirseniz, hello Windows PowerShell komut dosyaları uygun şekilde güncelleştirir.
    $lineMax|kaç tane tweet'leri hello betik okuma yapacak Hello değeri belirler. 100 tweet'leri tooread yaklaşık üç dakika sürer. Daha büyük bir sayı oluşturabilirsiniz ancak daha fazla zaman toodownload olur.

1. Tuşuna **F5** toorun hello komut dosyası. Geçici bir çözüm olarak sorunlarla karşılaşırsanız, tüm hello satırları seçin ve sonra basın **F8**.
2. "Tam!" göreceksiniz Merhaba Çıktı Hello sonunda. Kırmızı olarak herhangi bir hata iletisi görüntülenir.

Doğrulama yordamı hello çıktı dosyasını kontrol edebilirsiniz **/tutorials/twitter/data/tweets.txt**, bir Azure Depolama Gezgini veya Azure PowerShell kullanarak Azure Blob Depolama alanınızın üzerinde. Örnek Windows PowerShell komut dosyaları listeleme için bkz: [kullanım Blob storage Hdınsight ile][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>HiveQL komut dosyası oluşturma
Azure PowerShell kullanarak, birden çok HiveQL ifadelerini tek bir saat veya paket hello HiveQL deyimi bir komut dosyasına çalıştırabilirsiniz. Bu öğreticide, HiveQL betiğini oluşturur. Merhaba komut dosyasını karşıya yüklenen tooAzure Blob Depolama olması gerekir. Merhaba sonraki bölümde, Azure PowerShell kullanarak hello komut dosyası çalışır.

> [!NOTE]
> bir ortak Blob kapsayıcısında Hello Hive betik dosyası ve 10.000 tweet'leri içeren bir dosyayı karşıya yüklenmiş. Toouse hello karşıya yüklenen dosyaların istiyorsanız bu bölümü atlayabilirsiniz.

Merhaba HiveQL betiğini hello aşağıdakileri gerçekleştirir:

1. **Merhaba tweets_raw tablo bırakma** hello tablo zaten mevcut durumda.
2. **Merhaba tweets_raw Hive tablosu oluşturmak**. Bu geçici Hive yapılandırılmış tablosu için daha fazla extract hello verileri tutar, dönüştürme ve yükleme (ETL) işleme. Bölümleri hakkında daha fazla bilgi için bkz: [Hive öğretici][apache-hive-tutorial].
3. **Veri yükleme** hello kaynak klasörden /tutorials/twitter/data. iç içe geçmiş JSON biçiminde Hello büyük tweet'leri dataset geçici bir Hive tablosu yapısına şimdi dönüştürdü.
4. **Açılan hello tweet'leri tablo** hello tablo zaten mevcut durumda.
5. **Merhaba tweet'leri tablosu oluşturma**. Merhaba tweet'leri dataset karşı Hive kullanarak sorgulama yapabilirsiniz önce başka bir ETL işlemi toorun gerekir. Bu ETL işlemi hello "twitter_raw" tablosunda depolanan hello veriler için daha ayrıntılı bir tablo şemasını tanımlar.
6. **Üzerine yaz tablo ekleme**. Bu karmaşık Hive betiğini uzun MapReduce işleri bir dizi hello Hadoop küme tarafından tetiklersiniz. Veri kümesi ve hello boyutunuz kümenizin bağlı olarak, bu yaklaşık 10 dakika sürebilir.
7. **INSERT üzerine dizin**. Sorgu ve çıktı hello dataset tooa dosyasını çalıştırın. Bu sorgu "Azure" Merhaba sözcüğünü içeren çoğu tweet'leri gönderen Twitter kullanıcıların bir listesini döndürür.

**toocreate bir Hive betiği ve tooAzure yükleyin**

1. Windows PowerShell ISE açın.
2. Komut dosyası hello betik bölmesine aşağıdaki hello kopyalayın:

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Merhaba ilk iki değişkenleri hello komut dosyasında ayarlayın:

   | Değişken | Açıklama |
   | --- | --- |
   |  $clusterName |Toorun Merhaba uygulaması istediğiniz Hello Hdınsight küme adı girin. |
   |  $subscriptionID |Azure abonelik kimliğinizi girin |
   |  $sourceDataPath |Hello Azure Blob Depolama konumu hello Hive sorguları hello verileri nerede okur. Bu değişken toochange gerek yoktur. |
   |  $outputPath |Hello Azure Blob Depolama konumu hello sonuçları hello Hive sorguları yeri çıkarır. Bu değişken toochange gerek yoktur. |
   |  $hqlScriptFile |Başlangıç konumu ve hello hello HiveQL komut dosyasının dosya adı. Bu değişken toochange gerek yoktur. |
4. Tuşuna **F5** toorun hello komut dosyası. Geçici bir çözüm olarak sorunlarla karşılaşırsanız, tüm hello satırları seçin ve sonra basın **F8**.
5. "Tam!" göreceksiniz Merhaba Çıktı Hello sonunda. Kırmızı olarak herhangi bir hata iletisi görüntülenir.

Doğrulama yordamı hello çıktı dosyasını kontrol edebilirsiniz **/tutorials/twitter/twitter.hql**, bir Azure Depolama Gezgini veya Azure PowerShell kullanarak Azure Blob Depolama alanınızın üzerinde. Örnek Windows PowerShell komut dosyaları listeleme için bkz: [kullanım Blob storage Hdınsight ile][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Hive kullanarak twitter verilerini işlemek
Tüm hello hazırlık çalışması tamamladınız. Şimdi, hello Hive betiğini çağırma ve hello sonuçlarını kontrol edin.

### <a name="submit-a-hive-job"></a>Hive işi gönderin
Windows PowerShell komut dosyası toorun hello Hive betiğini aşağıdaki hello kullanın. Tooset hello ilk değişken gerekir.

> [!NOTE]
> toouse hello tweet'leri ve HiveQL betiğini hello son iki bölümlerde, kümesi $hqlScriptFile too"/tutorials/twitter/twitter.hql karşıya hello". toouse hello kaldırılmış olanları karşıya tooa ortak blob sizin için $hqlScriptFile çok Ayarla"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Merhaba sonuçları denetleyin
Windows PowerShell komut dosyası toocheck hello Hive iş çıktısı aşağıdaki hello kullanın. Tooset hello ilk iki değişkenleri gerekir.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> Merhaba Hive tablosu \001 alan sınırlayıcı hello gibi kullanır. Merhaba sınırlayıcı hello çıkışında görünür değil.

Merhaba çözümleme sonuçlarını Azure Blob depolama alanına yerleştirildi sonra verme hello veri tooan Azure SQL veritabanı/SQL sunucusu, Power Query kullanarak hello veri tooExcel dışarı veya hello Hive ODBC sürücüsü kullanarak uygulama toohello verilerinize bağlanın. Daha fazla bilgi için bkz: [Hdınsight ile kullanım Sqoop][hdinsight-use-sqoop], [Hdınsight kullanarak uçuş gecikme verileri analiz][hdinsight-analyze-flight-delay-data], [ Power Query ile Excel tooHDInsight bağlanmak][hdinsight-power-query], ve [hello Microsoft Hive ODBC sürücüsü ile bağlanma Excel tooHDInsight][hdinsight-hive-odbc].

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide biz nasıl tootransform yapılandırılmamış bir JSON veri kümesi içinde yapılandırılmış bir Hive tablosu tooquery keşfedin ve Twitter verilerini Azure üzerinde Hdınsight kullanarak çözümlemek gördünüz. toolearn daha bakın:

* [Hdınsight kullanmaya başlama][hdinsight-get-started]
* [Hdınsight'ta HBase ile gerçek zamanlı Twitter düşüncelerini çözümleme][hdinsight-hbase-twitter-sentiment]
* [Hdınsight kullanma uçuş gecikme verilerini çözümleme][hdinsight-analyze-flight-delay-data]
* [Excel tooHDInsight Power Query ile bağlanma][hdinsight-power-query]
* [Excel tooHDInsight hello Microsoft Hive ODBC sürücüsü ile bağlanma][hdinsight-hive-odbc]
* [Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
