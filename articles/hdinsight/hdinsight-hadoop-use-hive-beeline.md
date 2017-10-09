---
title: "Apache Hive - Azure Hdınsight ile Beeline aaaUse | Microsoft Docs"
description: "Hdınsight'ta Hadoop ile nasıl toouse hello Beeline istemci toorun Hive sorguları hakkında bilgi edinin. Beeline JDBC HiveServer2 ile çalışmaya yönelik bir yardımcı programdır."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive, hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Apache Hive ile Merhaba Beeline İstemcisi'ni kullanın

Bilgi nasıl toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive Hdınsight'ta sorgular.

Beeline hello baş Hdınsight küme düğümlerinde bulunan bir Hive istemcidir. Beeline JDBC tooconnect tooHiveServer2, Hdınsight kümenize üzerinde barındırılan bir hizmete kullanır. Ayrıca Beeline tooaccess Hive Hdınsight'ta uzaktan üzerinde kullanabileceğiniz Internet hello. Aşağıdaki tablonun hello Beeline ile kullanım için bağlantı dizelerini sağlar:

| Gelen Beeline çalıştırdığı | Parametreler |
| --- | --- | --- |
| Bir SSH bağlantı tooa headnode veya kenar düğümü | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Dış hello küme | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Değiştir `admin` hello küme oturum açma hesabıyla kümeniz için.
>
> Değiştir `password` hello küme oturum açma hesabının hello parolayla.
>
> Değiştir `clustername` Hdınsight kümenize hello adı.

## <a id="prereq"></a>Önkoşullar

* Linux tabanlı Hadoop Hdınsight kümesi üzerinde.

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Bir SSH istemcisi veya yerel bir Beeline istemci. Çoğu hello adımları bu belgede, bir SSH oturumu toohello kümeden Beeline kullandığınız varsayılır. Merhaba Beeline dış hello kümeden çalıştırma hakkında daha fazla bilgi için bkz [Beeline uzaktan kullanmak](#remote) bölümü.

    SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Beeline kullanın

1. Beeline başlatırken Hdınsight kümenize HiveServer2 için bir bağlantı dizesi belirtmeniz gerekir. toorun hello komutu dış hello kümeden hello küme oturum açma hesabı adı de sağlamanız gerekir (varsayılan `admin`) ve parola. Biçim ve parametreleri Tablo toofind hello bağlantı dizesi toouse aşağıdaki hello kullan:

    | Gelen Beeline çalıştırdığı | Parametreler |
    | --- | --- | --- |
    | Bir SSH bağlantı tooa headnode veya kenar düğümü | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Dış hello küme | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Örneğin, komutu aşağıdaki hello kullanılan toostart Beeline bir SSH oturumu toohello kümeden olabilir:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    Bu komut hello Beeline istemci başlar ve tooHiveServer2 hello küme baş düğümünde bağlanır. Konumundaki gelmesini Hello komutu işlemi tamamlandıktan sonra bir `jdbc:hive2://headnodehost:10001/>` istemi.

2. Beeline komutları ile başlar bir `!` karakter, örneğin `!help` Yardım gösterir. Ancak hello `!` bazı komutlar için atlanabilir. Örneğin, `help` de çalışır.

    Var olan bir `!sql`, hangi HiveQL ifadelerini kullanılan tooexecute değil. Ancak, önceki hello atlayabilirsiniz kadar sık HiveQL kullanılır `!sql`. Aşağıdaki iki deyimleri hello eşdeğerdir:

    ```hiveql
    !sql show tables;
    show tables;
    ```

    Yeni kümede, yalnızca bir tablo listelenir: **hivesampletable**.

3. Komut toodisplay hello şema hello hivesampletable için aşağıdaki hello kullan:

    ```hiveql
    describe hivesampletable;
    ```

    Bu komut, aşağıdaki bilgilerle hello döndürür:

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    Bu bilgiler hello tablodaki hello sütun açıklar. Biz bu verileri bazı sorgular gerçekleştirebilir olsa da, bunun yerine yeni bir tablo toodemonstrate nasıl oluşturalım Hive tooload veri ve şema uygulayın.

4. Aşağıdaki deyimleri toocreate adlı bir tablo hello girin **log4jLogs** hello Hdınsight kümesi ile sağlanan örnek verileri kullanarak:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

    * `DROP TABLE`-Hello tablo zaten varsa, bu silinir.

    * `CREATE EXTERNAL TABLE`-Oluşturur bir **dış** Hive tablo. Dış tablolara hello tablo tanımı kovanında yalnızca depolar. Merhaba veri hello özgün konumda kalır.

    * `ROW FORMAT`-Nasıl hello veri biçimlendirilir. Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.

    * `STORED AS TEXTFILE LOCATION`-Burada Hello veriler depolanır ve hangi dosya biçiminde.

    * `SELECT`-Tüm satırların sayımını seçer Burada sütun **t4** hello değeri içeren **[Hata]**. Bu sorgunun döndürdüğü değeri **3** bu değeri içeren üç satır olarak.

    * `INPUT__FILE__NAME LIKE '%.log'`-Hive tooapply hello şema tooall dosyaları hello dizininde çalışır. Bu durumda, başlangıç dizini hello şema eşleşmiyor dosyalarını içerir. tooprevent çöp veriler hello sonuçlarında, bu bildirimi bildirir Hive biz yalnızca veri biten dosyalarından döndürmesi gerektiğini. günlük.

  > [!NOTE]
  > Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır. Örneğin, bir otomatik veri karşıya yükleme işlemi veya bir MapReduce işlemi.
  >
  > Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.

    Merhaba, bu komutun metin benzer toohello aşağıdaki çıktı:

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. tooexit Beeline, kullanmak `!exit`.

## <a id="file"></a>Beeline toorun HiveQL dosyası kullanın

Adımları toocreate bir dosya çalıştırın Beeline kullanarak aşağıdaki hello kullanın.

1. Kullanım hello şu komutu toocreate adlı bir dosya **query.hql**:

    ```bash
    nano query.hql
    ```

2. Metin hello hello dosyasının içeriğini aşağıdaki hello kullanın. Bu sorgu adlı yeni bir 'iç' tablo oluşturur **günlüklerini**:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

    * **Tablo IF değil var oluşturmak** -hello tablo zaten mevcut değilse oluşturulur. Merhaba itibaren **dış** anahtar sözcüğü kullanılmaz, bu deyim bir iç tablosu oluşturur. İç tablolar hello Hive veri ambarında depolanır ve tamamen Hive tarafından yönetilir.
    * **AS ORC DEPOLANAN** -en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde hello verileri depolar. ORC biçimi Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.
    * **INSERT ÜZERİNE... SEÇİN** -hello satırları seçer **log4jLogs** içeren tablo **[Hata]**, eklemeleri veri hello hello sonra **günlüklerini** tablo.

    > [!NOTE]
    > Dış tablolara, bir iç tablosu bırakarak hello temel alınan veri de siler.

3. toosave hello dosya, kullanım **Ctrl**+**_X**, enter **Y**ve son olarak **Enter**.

4. Aşağıdaki Beeline kullanarak toorun hello dosyasına hello kullan:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Merhaba `-i` parametresi Beeline başlatır ve çalıştırmalarını hello hello query.hql dosyasındaki ifadelerini. Merhaba sorgu işlemi tamamlandıktan sonra hello gelmesini `jdbc:hive2://headnodehost:10001/>` istemi. Hello kullanarak bir dosyaya da çalıştırabilirsiniz `-f` hello sorgu tamamlandıktan sonra Beeline çıkar parametresi.

5. Merhaba tooverify **günlüklerini** tablosu oluşturuldu, tüm satırları hello deyimi tooreturn aşağıdaki hello kullan **günlüklerini**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    Üç veri satırı döndürülmesi, tüm içeren **[Hata]** sütun t4 içinde:

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Beeline uzaktan kullanın

Beeline yerel olarak yüklenmiş olması veya Docker resmin arkasını gibi kullanıyorsanız [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), şu parametreler hello kullanmanız gerekir:

* __Bağlantı dizesi__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __Küme oturum açma adı__:`-n admin`

* __Küme oturum açma parolasını__`-p 'password'`

Hello yerine `clustername` hello bağlantı dizesinde Hdınsight kümenize hello adı.

Değiştir `admin` küme oturum açma ve değiştirme hello adıyla `password` , küme oturum açma için hello parolayla.

## <a id="sparksql"></a>Spark ile Beeline kullanın

Spark refered tooas hello Spark Thrift sunucusunun görülür HiveServer2 kendi uygulamasını sağlar. Bu hizmet, Hive yerine Spark SQL tooresolve sorgularını kullanır ve sorgunuzu bağlı olarak daha iyi performans sağlayabilir.

Spark Hdınsight kümesinde, bağlantı noktası tooconnect toohello Spark Thrift sunucusunun `10002` yerine `10001`. Örneğin, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> değil erişilebilir üzerinden hello doğrudan internet hello Spark Thrift sunucusudur. Yalnızca bir SSH oturumunda tooit bağlanın veya içinde aynı Azure sanal ağ Hdınsight kümesi hello gibi hello.

## <a id="summary"></a><a id="nextsteps"></a>Sonraki adımlar

Hdınsight'ta Hive hakkında daha fazla genel bilgi için belge aşağıdaki hello bakın:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)

Hdınsight'ta Hadoop ile çalışabilirsiniz diğer yollar hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)

Tez Hive ile kullanıyorsanız, belgeleri aşağıdaki hello bakın:

* [Windows tabanlı Hdınsight üzerinde Hello Tez UI kullanın](hdinsight-debug-tez-ui.md)
* [Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın](hdinsight-debug-ambari-tez-view.md)

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

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
