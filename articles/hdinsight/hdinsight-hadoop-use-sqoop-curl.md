---
title: "Curl hdınsight'ta - Azure ile Hadoop Sqoop kullanma | Microsoft Docs"
description: "Sqoop Curl kullanarak hdınsight'a uzaktan göndermek öğrenin."
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
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Curl ile hdınsight'ta Hadoop ile Sqoop işleri çalıştırma
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Hdınsight Hadoop kümesinde Sqoop işlerini çalıştırmak için Curl kullanmayı öğrenin.

Curl çalıştırmak, izlemek ve Sqoop işleri sonuçları almak için ham HTTP isteklerini kullanarak Hdınsight ile nasıl etkileşim kurabileceğine göstermek için kullanılır. Bu, WebHCat REST (önceki adıyla Templeton da bilinir), Hdınsight küme tarafından sağlanan API'sini kullanarak çalışır.

> [!NOTE]
> Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni Hdınsight için, bkz: [Linux'ta Hdınsight kullanma hakkında bilgi](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu makaledeki adımları tamamlamak için aşağıdakiler gerekir:

* Hdınsight kümesi üzerinde Hadoop (Linux veya Windows tabanlı)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Curl kullanarak Sqoop işleri gönderme
> [!NOTE]
> Curl’ü veya WebHCat ile başka bir REST iletişimini kullanırken HDInsight küme yöneticisinin kullanıcı adı ve parolasını sağlayarak isteklerin kimliğini doğrulamanız gerekir. Ayrıca, sunucuya istek göndermek için kullanılan Tekdüzen Kaynak Tanımlayıcısı’nın (URI) bir parçası olarak küme adını kullanmanız gerekir.
> 
> Bu bölümdeki komutlar için **USERNAME** ifadesini küme kimliğini doğrulayacak kullanıcı ile, **PASSWORD** ifadesini ise kullanıcı hesabının parolası ile değiştirin. **CLUSTERNAME** değerini kümenizin adıyla değiştirin.
> 
> REST API’sinin güvenliği [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication) ile sağlanır. Kimlik bilgilerinizin sunucuya güvenli bir şekilde gönderilmesi için istekleri her zaman Güvenli HTTP (HTTPS) kullanarak yapmanız gerekir.
> 
> 

1. HDInsight kümenize bağlanabildiğinizi doğrulamak için bir komut satırında aşağıdaki komutu kullanın:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Aşağıdakine benzer bir yanıt almanız gerekir:
   
        {"status":"ok","version":"v1"}
   
    Bu komutta kullanılan parametreler aşağıdaki gibidir:
   
   * **-u** - İstek kimliğini doğrulamak için kullanılan kullanıcı adı ve parola.
   * **-G** - Bunun bir GET isteği olduğunu belirtir.
     
     URL'nin başına **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, tüm istekler için aynı olacaktır. Yol **/status**, sunucu için istek WebHCat (Templeton olarak da bilinir) durumuna döndürmek için olduğunu belirtir. 
2. Sqoop işi göndermek için aşağıdakileri kullanın:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    Bu komutta kullanılan parametreler aşağıdaki gibidir:

    * **-d** - bu yana `-G` kullanılmaz, istek varsayılan olarak, POST yöntemi. `-d`istekle birlikte gönderilen veri değerleri belirtir.

        * **User.Name** -komutu çalıştıran kullanıcının.

        * **komut** -Sqoop komutun yürütülmesi için.

        * **statusdir** -bu iş için durumu yazılır dizin.

    Bu komut, iş durumunu denetlemek için kullanılan bir iş kimliği döndürmelidir.

        {"id":"job_1415651640909_0026"}

1. İş durumunu denetlemek için aşağıdaki komutu kullanın. Değiştir **JOBID** önceki adımda döndürülen değer. Örneğin, dönüş değeri `{"id":"job_1415651640909_0026"}`, ardından **JOBID** olacaktır `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    İş tamamlandı, durum olacaktır **başarılı**.
   
   > [!NOTE]
   > Bu Curl isteği iş hakkındaki bilgileri ile bir JavaScript nesne gösterimi (JSON) belgesini döndürür; jq yalnızca durum değeri almak için kullanılır.
   > 
   > 
2. İş durumu olarak değiştirildi sonra **başarılı**, Azure Blob depolama alanından iş sonuçlarını alabilirsiniz. `statusdir` Sorguyla geçirilen parametre içeren çıkış dosyasının; bu durumda, konumu **wasb: / / / örnek/curl**. Bu adres işinde çıktısını depolar **örnek/curl** Hdınsight küme tarafından kullanılan varsayılan depolama kapsayıcısı üzerinde dizin.
   
    Liste ve kullanarak bu dosyaları indirmek [Azure CLI](../cli-install-nodejs.md). Örneğin, liste dosyalarında için **örnek/curl**, aşağıdaki komutu kullanın:
   
        azure storage blob list <container-name> example/curl
   
    Bir dosyayı indirmek için aşağıdakileri kullanın:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Blob içeriyor. kullanarak depolama hesabı adı ya da belirtmeniz gerekir `-a` ve `-k` parametreleri veya kümesi **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_erişim\_anahtar** ortam değişkenleri. Bkz: < bir href = "hdınsight-karşıya yükleme-data.md" target = "_blank" daha fazla bilgi için.
   > 
   > 

## <a name="limitations"></a>Sınırlamalar
* Toplu export - ile Linux tabanlı Hdınsight, Microsoft SQL Server veya Azure SQL veritabanı için verileri dışa aktarmak için kullanılan Sqoop bağlayıcı toplu eklemeler şu anda desteklemiyor.
* -Kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop, INSERT işlemlerine toplu işleme yerine birden çok eklemeleri gerçekleştirir.

## <a name="summary"></a>Özet
Bu belgede gösterildiği gibi çalıştırın, izlemek ve Hdınsight kümenize Sqoop işleri sonuçlarını görüntülemek için ham bir HTTP isteği'ni kullanabilirsiniz.

Bu makalede kullanılan REST arabirimi hakkında daha fazla bilgi için bkz: <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API Kılavuzu</a>.

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


