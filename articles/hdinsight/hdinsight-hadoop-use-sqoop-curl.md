---
title: "aaaUse Hadoop Sqoop Curl hdınsight'ta - Azure ile | Microsoft Docs"
description: "Nasıl tooremotely gönderme Curl kullanarak Sqoop işleri tooHDInsight öğrenin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Curl ile hdınsight'ta Hadoop ile Sqoop işleri çalıştırma
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Bir Hadoop toouse Curl toorun Sqoop işlerine Hdınsight'ta nasıl küme öğrenin.

Curl ham HTTP isteklerini toorun, İzleyici ve Sqoop işleri alma hello sonuçlarını kullanarak Hdınsight ile nasıl etkileşim kurabileceğine kullanılan toodemonstrate ' dir. Bu, hello WebHCat REST Hdınsight küme tarafından sağlanan API (önceki adıyla Templeton da bilinir) kullanarak çalışır.

> [!NOTE]
> Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni tooHDInsight olan, bkz: [Linux'ta Hdınsight kullanma hakkında bilgi](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir:

* Hdınsight kümesi üzerinde Hadoop (Linux veya Windows tabanlı)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Curl kullanarak Sqoop işleri gönderme
> [!NOTE]
> Curl'ü veya başka bir REST iletişimini WebHCat ile kullanırken, hello kullanıcı adı ve parola hello Hdınsight küme yöneticisinin sağlayarak hello istekleri kimliğini doğrulaması gerekir. Merhaba Tekdüzen Kaynak Tanımlayıcısı (URI) bir parçası toosend hello istekleri toohello sunucu kullanılan gibi hello küme adını kullanmanız gerekir.
> 
> Bu bölümdeki Hello komutlar için Değiştir **kullanıcıadı** hello kullanıcı tooauthenticate toohello küme ve Değiştir **parola** hello hello kullanıcı hesabının parolasını ile. Değiştir **CLUSTERNAME** kümenizin hello ada sahip.
> 
> Merhaba REST API aracılığıyla güvenli [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication). Her zaman güvenli HTTP (toohelp olun kimlik bilgilerinizi toohello sunucu güvenli bir şekilde gönderilir HTTPS) kullanarak istekleri yapmanız.
> 
> 

1. Bir komut satırından tooyour Hdınsight kümesi bağlanabilir komutu tooverify aşağıdaki hello kullan:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Yanıt benzer toohello aşağıdaki almanız gerekir:
   
        {"status":"ok","version":"v1"}
   
    Bu komutta kullanılan hello parametreler aşağıdaki gibidir:
   
   * **-u** -hello kullanıcı adı ve parola kullanılan tooauthenticate hello isteği.
   * **-G** - Bunun bir GET isteği olduğunu belirtir.
     
     Merhaba URL'sini başlayan hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, aynı tüm istekler için hello olacaktır. Merhaba yolu **/status**, o hello isteği tooreturn WebHCat (Templeton olarak da bilinir) durumunu hello sunucusu için gösterir. 
2. Toosubmit sqoop işi aşağıdaki hello kullan:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    Bu komutta kullanılan hello parametreler aşağıdaki gibidir:

    * **-d** - bu yana `-G` kullanılmaz, hello isteği varsayılan olarak toohello POST yöntemi. `-d`gönderilen Merhaba veri değerleri ile Merhaba isteğini belirtir.

        * **User.Name** -hello komutu çalıştıran hello kullanıcı.

        * **komut** -Sqoop komutu tooexecute hello.

        * **statusdir** -bu iş için durumu hello hello dizinine yazılacak.

    Bu komut, kullanılan toocheck hello hello işinin durumunu olabilir bir iş kimliği döndürmelidir.

        {"id":"job_1415651640909_0026"}

1. Merhaba işinin komutu aşağıdaki kullanım hello toocheck hello durumu. Değiştir **JOBID** hello önceki adımda döndürülen hello değerine sahip. Örneğin, hello değeri döndürür `{"id":"job_1415651640909_0026"}`, ardından **JOBID** olacaktır `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Merhaba işi tamamlandı, hello durumu olacaktır **başarılı**.
   
   > [!NOTE]
   > Bu Curl istek hello işi hakkındaki bilgileri ile bir JavaScript nesne gösterimi (JSON) belgesini döndürür; jq kullanılan tooretrieve yalnızca hello durum değeri.
   > 
   > 
2. Merhaba işin Hello durumu çok değişti sonra**başarılı**, Azure Blob depolama alanından hello iş hello sonuçlarını alabilirsiniz. Merhaba `statusdir` hello sorguyla geçirilen parametre içeren hello çıkış dosyasının; bu durumda, hello konumu **wasb: / / / örnek/curl**. Bu adresi hello hello çıktı hello işinin saklar **örnek/curl** Hdınsight küme tarafından kullanılan hello varsayılan depolama kapsayıcısı üzerinde dizin.
   
    Liste ve hello kullanarak bu dosyaları indirmek [Azure CLI](../cli-install-nodejs.md). Örneğin, içinde toolist dosyaları **örnek/curl**, hello aşağıdaki komutu kullanın:
   
        azure storage blob list <container-name> example/curl
   
    bir dosya toodownload hello aşağıdakileri kullanın:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Merhaba blob içeriyor. hello kullanarak hello depolama hesabı adı ya da belirtmeniz gerekir `-a` ve `-k` parametreleri veya kümesi hello **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_erişim\_anahtar** ortam değişkenleri. Bkz: < bir href = "hdınsight-karşıya yükleme-data.md" target = "_blank" daha fazla bilgi için.
   > 
   > 

## <a name="limitations"></a>Sınırlamalar
* Toplu export - ile Linux tabanlı Hdınsight, hello Sqoop kullanılan bağlayıcı tooexport veri tooMicrosoft SQL Server ya da Azure SQL veritabanı toplu eklemeler şu anda desteklemiyor.
* -Hello kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop hello INSERT işlemlerine toplu işleme yerine birden çok eklemeleri gerçekleştirir.

## <a name="summary"></a>Özet
Bu belgede gösterildiği gibi Hdınsight kümesinde bir ham HTTP isteği toorun, İzleyici ve Sqoop işlerin hello sonuçları görüntüle kullanabilirsiniz.

Bu makalede kullanılan hello REST arabirimi hakkında daha fazla bilgi için bkz: Merhaba <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API Kılavuzu</a>.

## <a name="next-steps"></a>Sonraki adımlar
Hdınsight ile Hive hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile Sqoop kullanma](hdinsight-use-sqoop.md)

Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)

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


