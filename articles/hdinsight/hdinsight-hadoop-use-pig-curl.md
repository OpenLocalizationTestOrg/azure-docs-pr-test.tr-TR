---
title: "aaaUse REST hdınsight'ta - Azure ile Hadoop Pig | Microsoft Docs"
description: "Azure Hdınsight'ta nasıl toouse REST toorun Pig Latin işlerine bir Hadoop küme öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>Pig işleri, REST kullanarak Hdınsight'ta Hadoop ile çalıştırın

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

REST istekleri tooan Azure Hdınsight kümesi yaparak toorun Pig Latin nasıl işler öğrenin. Curl hello WebHCat REST API kullanarak Hdınsight ile nasıl etkileşim kullanılan toodemonstrate ' dir.

> [!NOTE]
> Zaten Linux tabanlı Hadoop sunucuları kullandıysanız, ancak yeni tooHDInsight olan, bkz: [Linux tabanlı Hdınsight ipuçları](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Önkoşullar

* Azure Hdınsight (Hadoop hdınsight) kümesi (Linux tabanlı veya Windows tabanlı)

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Curl](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Curl kullanarak pig işleri çalıştırma

> [!NOTE]
> Merhaba REST API aracılığıyla güvenli [temel erişimi kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication). Her zaman istekleri kimlik bilgilerinizi toohello sunucu güvenli bir şekilde gönderilir Güvenli HTTP (HTTPS) tooensure kullanarak yapın.
>
> Merhaba komutları bu bölümde, kullanırken değiştirin `USERNAME` hello kullanıcı tooauthenticate toohello küme ve Değiştir ile `PASSWORD` hello hello kullanıcı hesabının parolasını ile. Değiştir `CLUSTERNAME` kümenizin hello ada sahip.
>


1. Bir komut satırından tooyour Hdınsight kümesi bağlanabilir komutu tooverify aşağıdaki hello kullan:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    JSON yanıt aşağıdaki hello almanız gerekir:

        {"status":"ok","version":"v1"}

    Bu komutta kullanılan hello parametreler aşağıdaki gibidir:

    * **-u**: hello kullanıcı adı ve parola kullanılan tooauthenticate hello isteği
    * **-G**: Bu isteği bir GET isteği olduğunu gösterir

     Merhaba URL'sini başlayan hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, olan hello aynı tüm istekler için. Merhaba yolu **/status**, o hello isteği tooreturn hello WebHCat (Templeton olarak da bilinir) durumunu hello sunucusu için gösterir.

2. Aşağıdaki kod toosubmit Pig Latin iş toohello küme hello kullan:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    Bu komutta kullanılan hello parametreler aşağıdaki gibidir:

    * **-d**: çünkü `-G` kullanılmaz, hello isteği varsayılan olarak toohello POST yöntemi. `-d`gönderilen Merhaba veri değerleri ile Merhaba isteğini belirtir.

    * **User.Name**: hello komutu çalıştıran hello kullanıcı
    * **yürütme**: Pig Latin deyimleri tooexecute hello
    * **statusdir**: Bu iş için durumu hello hello dizin yazılır

    > [!NOTE]
    > Pig Latin deyimlerinde Hello alanları tarafından hello değiştirilir fark `+` karakter Curl ile kullanıldığında.

    Bu komut, kullanılan toocheck hello hello işinin durumunu örneğin olabilir bir iş kimliği döndürmesi gerekir:

        {"id":"job_1415651640909_0026"}

3. Merhaba işinin komutu aşağıdaki kullanım hello toocheck hello durumu

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     Değiştir `JOBID` hello önceki adımda döndürülen hello değerine sahip. Örneğin, hello değeri döndürür `{"id":"job_1415651640909_0026"}`, ardından `JOBID` olan `job_1415651640909_0026`.

    Merhaba işi tamamlanmadan hello durumu varsa, **başarılı**.

    > [!NOTE]
    > JavaScript nesne gösterimi (JSON) belge hello iş ve jq hakkında bilgi döndürür kullanılan tooretrieve olan bu Curl isteği yalnızca hello durum değeri.

## <a id="results"></a>Sonuçları Görüntüle

Ne zaman hello iş hello durumu değişti çok**başarılı**, hello iş hello sonuçlarını alabilirsiniz. Merhaba `statusdir` hello sorguyla geçirilen parametre içeren hello çıkış dosyasının; bu durumda, hello konumu `/example/pigcurl`.

Hdınsight Azure Storage veya Azure Data Lake Store hello varsayılan veri deposu olarak kullanabilirsiniz. Hangisinin bağlı olarak kullandığınız hello verilerini çeşitli şekillerde tooget vardır. Daha fazla bilgi için hello hello depolama bölümüne bakın [Linux tabanlı Hdınsight bilgi](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) belge.

## <a id="summary"></a>Özet

Bu belgede gösterildiği gibi Hdınsight kümesinde bir ham HTTP isteği toorun, İzleyici ve Pig işleri görüntüle hello sonucu kullanabilirsiniz.

Bu makalede kullanılan hello REST arabirimi hakkında daha fazla bilgi için bkz: Merhaba [WebHCat başvuru](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

## <a id="nextsteps"></a>Sonraki adımlar

Hdınsight Pig hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)
