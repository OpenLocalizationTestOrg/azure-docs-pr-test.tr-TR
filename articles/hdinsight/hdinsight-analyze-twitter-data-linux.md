---
title: "Apache Hive - Azure Hdınsight ile Twitter veri aaaAnalyze | Microsoft Docs"
description: "Nasıl toouse Hive ve Hadoop Hdınsight tootransform ham TWitter verilerini aranabilir Hive tabloya bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>Twitter verilerini Hdınsight'ta Hive ve Hadoop kullanarak çözümleme

Bilgi nasıl toouse Apache Hive tooprocess Twitter veri. Merhaba, belirli bir sözcük içeren çoğu tweet'leri hello gönderen Twitter kullanıcıların listesini sonucudur.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Hdınsight 3.6 üzerinde test edilmiş.
>
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="get-hello-data"></a>Merhaba Veri Al

Twitter tooretrieve hello verir [her tweet için veri](https://dev.twitter.com/docs/platform-objects/tweets) bir REST API'si aracılığıyla JavaScript nesne gösterimi (JSON) belgesi olarak. [OAuth](http://oauth.net) kimlik doğrulaması toohello API için gereklidir.

### <a name="create-a-twitter-application"></a>Bir Twitter uygulaması oluşturma

1. Bir web tarayıcısından çok oturum[https://apps.twitter.com/](https://apps.twitter.com/). Merhaba tıklatın **kaydolma şimdi** bir Twitter hesabı yoksa bağlantı.

2. Tıklatın **yeni uygulama oluştur**.

3. Girin **adı**, **açıklama**, **Web sitesi**. Hello için bir URL yukarı yapabileceğiniz **Web sitesi** alan. Aşağıdaki tablonun hello bazı örnek değerleri toouse gösterir:

   | Alan | Değer |
   |:--- |:--- |
   | Ad |MyHDInsightApp |
   | Açıklama |MyHDInsightApp |
   | Web sitesi |http://www.myhdinsightapp.com |

4. Denetleme **Evet, kabul ediyorum**ve ardından **Twitter uygulamanızı oluşturma**.

5. Merhaba tıklatın **izinleri** sekmesini hello varsayılan izni **salt okunur**.

6. Merhaba tıklatın **anahtarları ve erişim belirteçleri** sekmesi.

7. Tıklatın **my erişim belirteci oluşturma**.

8. Tıklatın **Test OAuth** hello sayfasının hello sağ üst köşesindeki.

9. Yazma **tüketici anahtarı**, **tüketici gizli**, **erişim belirteci**, ve **erişim belirteci gizli anahtarı**.

### <a name="download-tweets"></a>Tweet'leri indirin

Python kodu aşağıdaki hello indirmeleri 10.000 tweet'leri Twitter ve bunları kaydetme adlı tooa dosya **tweets.txt**.

> [!NOTE]
> Python zaten yüklemenizden sonra aşağıdaki adımları hello hello Hdınsight kümesinde gerçekleştirilir.

1. SSH kullanarak toohello Hdınsight kümesine bağlanın:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Kullanım hello aşağıdaki komutları tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)ve diğer gerekli paketleri:

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. Kullanım hello şu komutu toocreate adlı bir dosya **gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. Metin hello Merhaba içeriğine aşağıdaki kullanım hello **gettweets.py** dosyası:

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > Twitter uygulamanızdan hello bilgilerle öğeleri aşağıdaki hello Hello yer tutucu metnini değiştirin:
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. Kullanım **Ctrl + X**, ardından **Y** toosave hello dosya.

7. Aşağıdaki komut toorun hello dosyasına hello kullanın ve tweet'leri karşıdan yükleyin:

    ```bash
    python gettweets.py
    ```

    Bir İlerleme göstergesi görünür. Bu too100% tweet'leri indirilir hello sayılır.

   > [!NOTE]
   > Merhaba ilerleme çubuğu tooadvance uzun bir süredir sürüyorsa hello filtre tootrack oluşturan eğilim konuları değiştirmeniz gerekir. Filtre hello konuda hakkında birçok tweetler olduğunda gerekli 10000 tweet'leri hello hızlı bir şekilde alabilir.

### <a name="upload-hello-data"></a>Merhaba veri yükleme

tooupload hello veri tooHDInsight depolama, aşağıdaki komutları kullanın hello:

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

Bu komutlar hello veri hello kümedeki tüm düğümlerin erişebildiği bir konuma depolayın.

## <a name="run-hello-hiveql-job"></a>Merhaba HiveQL işini çalıştır

1. Komut toocreate aşağıdaki HiveQL ifadelerini içeren bir dosyasına hello kullan:

   ```bash
   nano twitter.hql
   ```

    Metin hello hello dosyasının içeriğini aşağıdaki hello kullan:

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
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
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
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
   ```

2. Basın **Ctrl + X**, tuşuna basarak **Y** toosave hello dosya.
3. Aşağıdaki HiveQL hello dosyasında yer alan komut toorun hello hello kullan:

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    Çalıştırır hello hello bu komut **twitter.hql** dosya. Gördüğünüz Hello sorgu tamamlandıktan sonra bir `jdbc:hive2//localhost:10001/>` istemi.

4. Merhaba beeline isteminden veri içeri aktarılmış sorgu tooverify aşağıdaki hello kullan:

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    Bu sorgunun döndürdüğü hello sözcüğünü içeren 10 tweet'leri maksimum **Azure** hello ileti metin.

## <a name="next-steps"></a>Sonraki adımlar

Öğrendiğiniz nasıl tootransform yapılandırılmış bir Hive tablosu yapılandırılmamış bir JSON veri kümesi. toolearn, hdınsight'ta Hive hakkında daha fazla belgeleri aşağıdaki hello bakın:

* [Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Hdınsight kullanma uçuş gecikme verilerini çözümleme](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
