---
title: "aaaUse MapReduce ve Curl hdınsight'ta - Azure Hadoop ile | Microsoft Docs"
description: "Tooremotely çalışma şeklini MapReduce işleri Hadoop ile Hdınsight'ta Curl kullanarak öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>REST kullanarak Hdınsight'ta Hadoop ile MapReduce işleri çalıştırma

Nasıl Hdınsight kümesinde bir hadoop'ta toouse hello WebHCat REST API toorun MapReduce işleri öğrenin. Curl ham HTTP isteklerini toorun MapReduce işleri kullanarak Hdınsight ile nasıl etkileşim kurabileceğine kullanılan toodemonstrate ' dir.

> [!NOTE]
> Linux tabanlı Hadoop sunucuları kullanarak bilginiz, ancak yeni tooHDInsight, hello bkz [gerekenleri hdınsight'ta Linux tabanlı Hadoop hakkında tooknow](hdinsight-hadoop-linux-information.md) belge.


## <a id="prereq"></a>Önkoşullar

* Hdınsight kümesi Hadoop'ta
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Curl kullanarak MapReduce işleri çalıştırma

> [!NOTE]
> WebHCat ile Curl veya başka bir REST iletişimini kullanırken hello Hdınsight küme yönetici kullanıcı adını ve parolasını sağlayarak hello istekleri kimliğini doğrulaması gerekir. Merhaba kullanılan toosend hello istekleri toohello sunucusu URI bir parçası olarak hello küme adını kullanmanız gerekir.
>
> Bu bölümdeki Hello komutlar için Değiştir **kullanıcıadı** hello kullanıcı tooauthenticate toohello kümesi ile ve **parola** hello hello kullanıcı hesabının parolasını ile. Değiştir **CLUSTERNAME** kümenizin hello ada sahip.
>
> Merhaba REST API kullanarak korunuyor [temel erişimi kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication). Ayrıca, kimlik bilgilerinizi toohello sunucu güvenli bir şekilde gönderilir HTTPS tooensure kullanarak istekleri her zaman yapmanız gerekir.


1. Bir komut satırından tooyour Hdınsight kümesi bağlanabilir komutu tooverify aşağıdaki hello kullan:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    JSON izleyen bir yanıt benzer toohello almanız gerekir:

        {"status":"ok","version":"v1"}

    Bu komutta kullanılan hello parametreler aşağıdaki gibidir:

   * **-u**: hello kullanıcı adı ve parola kullanılan tooauthenticate hello isteği gösterir
   * **-G**: Bu işlem bir GET isteği olduğunu gösterir

     URI, Merhaba başlayan hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, olan hello aynı tüm istekler için.

2. toosubmit bir MapReduce işi hello aşağıdaki komutu kullanın:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    Merhaba URI (/ mapreduce/jar) Hello sonuna bu istek bir sınıftan jar dosyasındaki bir MapReduce işi başlatır WebHCat söyler. Bu komutta kullanılan hello parametreler aşağıdaki gibidir:

   * **-d**: `-G` toohello POST yöntemini hello isteği Varsayılanları şekilde, kullanılmaz. `-d`gönderilen Merhaba veri değerleri ile Merhaba isteğini belirtir.
    * **User.Name**: hello komutu çalıştıran hello kullanıcı
    * **jar**: sınıf toobe içeren hello jar dosyasını hello konumunu çalıştı
    * **sınıf**: Merhaba hello MapReduce mantığı içeren sınıfı
    * **arg**: hello bağımsız değişkenleri toobe toohello MapReduce işi geçirildi. Bu durumda, hello hello çıktı için kullanılan metin dosyası ve hello dizin girişi

     Bu komut, kullanılan toocheck hello hello işinin durumunu olabilir bir iş kimliği döndürmesi gerekir:

       {"ID": "job_1415651640909_0026"}

3. Merhaba işinin komutu aşağıdaki kullanım hello toocheck hello durumu:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Hello yerine **JOBID** hello önceki adımda döndürülen hello değerine sahip. Örneğin, hello değeri döndürür `{"id":"job_1415651640909_0026"}`, ardından JOBID olacaktır hello `job_1415651640909_0026`.

    Merhaba işi tamamlandıktan hello durumu döndürülür `SUCCEEDED`.

   > [!NOTE]
   > Bu Curl isteği bir JSON belgesi hello işi hakkında bilgi döndürür. Jq kullanılan tooretrieve yalnızca hello durum değeri.

4. Ne zaman hello iş hello durumu değişti çok`SUCCEEDED`, Azure Blob depolama alanından hello iş hello sonuçlarını alabilirsiniz. Merhaba `statusdir` hello sorguyla geçirilen parametre hello hello çıkış dosyasının konumunu içerir. Bu örnekte, hello konumdur `/example/curl`. Bu adres hello çıktısını hello hello kümeleri varsayılan depolama depolar `/example/curl`.

Liste ve hello kullanarak bu dosyaları indirmek [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Merhaba hello Azure CLI bloblarından ile çalışma hakkında daha fazla bilgi için bkz: [kullanma hello Azure Storage ile Azure CLI 2.0](../storage/common/storage-azure-cli.md#create-and-manage-blobs) belge.

## <a id="nextsteps"></a>Sonraki adımlar

Hdınsight'ta MapReduce işleri hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)

Bu makalede kullanılan hello REST arabirimi hakkında daha fazla bilgi için bkz: Merhaba [WebHCat başvuru](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).
