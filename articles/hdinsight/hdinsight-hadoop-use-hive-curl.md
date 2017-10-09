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
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>REST kullanarak hdınsight'ta Hadoop ile Hive sorguları çalıştırma

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Toouse hello WebHCat REST API toorun Hive Hadoop ile Azure Hdınsight kümesinde nasıl sorgular öğrenin.

[Curl](http://curl.haxx.se/) nasıl, etkileşimli olarak çalışabilir Hdınsight ile ham HTTP isteklerini kullanarak kullanılan toodemonstrate değil. Merhaba [jq](http://stedolan.github.io/jq/) programıdır kullanılan tooprocess hello JSON verilerini REST isteklerinden döndürdü.

> [!NOTE]
> Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni tooHDInsight hello bkz [gerekenleri Linux tabanlı hdınsight'ta Hadoop hakkında tooknow](hdinsight-hadoop-linux-information.md) belge.

## <a id="curl"></a>Hive sorgularını çalıştırma

> [!NOTE]
> Curl'ü veya başka bir REST iletişimini WebHCat ile kullanırken, hello kullanıcı adı ve parola hello Hdınsight küme yöneticisinin sağlayarak hello istekleri kimliğini doğrulaması gerekir.
>
> Bu bölümdeki Hello komutlar için Değiştir **kullanıcıadı** hello kullanıcı tooauthenticate toohello küme ve Değiştir **parola** hello hello kullanıcı hesabının parolasını ile. Değiştir **CLUSTERNAME** kümenizin hello ada sahip.
>
> Merhaba REST API aracılığıyla güvenli [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication). toohelp kimlik bilgilerinizi güvenli olduğundan emin olun toohello sunucu gönderilen, her zaman güvenli HTTP (HTTPS) kullanarak isteklerde.

1. Bir komut satırından tooyour Hdınsight kümesi bağlanabilir komutu tooverify aşağıdaki hello kullan:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Metin izleyen bir yanıt benzer toohello alırsınız:

        {"status":"ok","version":"v1"}

    Bu komutta kullanılan hello parametreler aşağıdaki gibidir:

   * **-u** -hello kullanıcı adı ve parola kullanılan tooauthenticate hello isteği.
   * **-G** -bu isteği alma işlemi olduğunu gösterir.

     Merhaba URL'sini başlayan hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, olan hello aynı tüm istekler için. Merhaba yolu **/status**, o hello isteği tooreturn WebHCat (Templeton olarak da bilinir) durumunu hello sunucusu için gösterir. Hive hello sürümü komutu aşağıdaki hello kullanarak da isteğinde bulunabilirsiniz:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     Bu istek metnini izleyen bir yanıt benzer toohello döndürür:

       {"modülünde": "hive", "Sürüm": "0.13.0.2.1.6.0-2103"}

2. Toocreate adlı bir tablo aşağıdaki kullanım hello **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Bu istekle kullanılan parametreler aşağıdaki hello:

   * **-d** - bu yana `-G` kullanılmaz, hello isteği varsayılan olarak toohello POST yöntemi. `-d`gönderilen Merhaba veri değerleri ile Merhaba isteğini belirtir.

     * **User.Name** -hello komutu çalıştıran hello kullanıcı.
     * **yürütme** -HiveQL ifadelerini tooexecute hello.
     * **statusdir** -bu iş için durumu hello hello dizin yazılır.

     Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:
   * **DROP TABLE** -hello tablo zaten silinmiş.
   * **Dış tablo oluştur** -kovanında yeni bir 'external' tablo oluşturur. Dış tablolara yalnızca hello tablo tanımı kovanında depolar. Merhaba veri hello özgün konumda kalır.

     > [!NOTE]
     > Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır. Örneğin, bir otomatik veri karşıya yükleme işlemi veya başka bir MapReduce işlemi.
     >
     > Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.

   * **SATIR biçimi** - hello veri biçimlendirilmiş nasıl. Her günlüğüne Hello alanlar boşlukla ayrılır.
   * **AS TEXTFILE konumu DEPOLANAN** - hello veriler burada (Merhaba örnek/veri dizini) ve metin olarak depolanır.
   * **SEÇİN** -tüm satırların sayımını seçer Burada sütun **t4** hello değeri içeren **[Hata]**. Bu ifade değerini döndürür **3** bu değeri içeren üç satır olarak.

     > [!NOTE]
     > Merhaba alanları HiveQL ifadelerini arasında hello tarafından değiştirilir fark `+` karakter Curl ile kullanıldığında. Merhaba sınırlayıcı gibi bir alanı içeren tırnak içine alınmış değerler değiştirilmemişse tarafından `+`.

   * **'% 25.log' INPUT__FILE__NAME gibi** - biten bu deyimi sınırları hello arama tooonly dosyaları kullanma. günlük.

     > [!NOTE]
     > Merhaba `%25` hello gerçek koşul hello URL kodlanmış form %, olduğundan `like '%.log'`. Merhaba % toobe URL kodlanmış, aynıdır URL'lerde özel karakter olarak kabul edilir.

     Bu komut, kullanılan toocheck hello hello işinin durumunu olabilir bir iş kimliği döndürmelidir.

       {"ID": "job_1415651640909_0026"}

3. Merhaba işinin komutu aşağıdaki kullanım hello toocheck hello durumu:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Değiştir **JOBID** hello önceki adımda döndürülen hello değerine sahip. Örneğin, hello değeri döndürür `{"id":"job_1415651640909_0026"}`, ardından **JOBID** olacaktır `job_1415651640909_0026`.

    Merhaba işi tamamlanmadan hello durumu varsa, **başarılı**.

   > [!NOTE]
   > Bu Curl istek JavaScript nesne gösterimi (JSON) belge hello işi hakkında bilgi döndürür. Jq kullanılan tooretrieve yalnızca hello durum değeri.

4. Merhaba işin Hello durumu çok değişti sonra**başarılı**, Azure Blob depolama alanından hello iş hello sonuçlarını alabilirsiniz. Merhaba `statusdir` hello sorguyla geçirilen parametre içeren hello çıkış dosyasının; bu durumda, hello konumu **/örnek/curl**. Bu adres hello çıktı hello depolar **örnek/curl** hello dizininde kümeleri varsayılan depolama.

    Liste ve hello kullanarak bu dosyaları indirmek [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Merhaba hello Azure CLI Azure Storage ile kullanma hakkında daha fazla bilgi için bkz: [Azure Storage ile Azure CLI 2.0 Kullan](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) belge.

5. Aşağıdaki deyimleri toocreate adlı yeni bir 'iç' tablo kullanım hello **günlüklerini**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

   * **Tablo IF değil var oluşturmak** -zaten yoksa, bir tablo oluşturur. Bu bildirimi hello Hive veri ambarında depolanır ve Hive tamamen yönetilen bir iç bir tablo oluşturur.

     > [!NOTE]
     > Dış tablolara, bir iç tablosu bırakarak hello temel alınan veri de siler.

   * **AS ORC DEPOLANAN** -en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde hello verileri depolar. ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.
   * **INSERT ÜZERİNE... SEÇİN** -hello satırları seçer **log4jLogs** içeren tablo **[Hata]**, eklemeleri veri hello hello sonra **günlüklerini** tablo.
   * **SEÇİN** -hello yeni tüm satırları seçer **günlüklerini** tablo.

6. Kullanım hello iş kimliği toocheck hello hello işinin durumunu döndürdü. Başarılı olduktan sonra hello toodownload ve görünüm hello sonuçları daha önce açıklandığı gibi Azure CLI kullanın. Merhaba çıktı, her biri içeren üç satırları içermelidir **[Hata]**.

## <a id="nextsteps"></a>Sonraki adımlar

Hdınsight ile Hive hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)

Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)

Tez Hive ile kullanıyorsanız, belgeleri hata ayıklama bilgileri için aşağıdaki hello bakın:

* [Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın](hdinsight-debug-ambari-tez-view.md)

Merhaba hello bu belgede kullanılan REST API hakkında daha fazla bilgi için bkz: [WebHCat başvuru](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) belge.

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


