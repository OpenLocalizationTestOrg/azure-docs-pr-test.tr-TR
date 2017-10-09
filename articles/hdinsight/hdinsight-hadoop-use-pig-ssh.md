---
title: "Hdınsight kümesinde - Azure SSH ile Hadoop Pig aaaUse | Microsoft Docs"
description: "Bilgi tooa Linux tabanlı Hadoop kümesi SSH ile nasıl bağlanacağını ve ardından kullanımı hello Pig komutu toorun Pig Latin deyimleri etkileşimli olarak veya toplu olarak iş."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Merhaba Pig komutu (SSH) ile Linux tabanlı kümesi pig işleri çalıştırma

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Toointeractively çalışma şeklini Pig işleri SSH bağlantı tooyour Hdınsight kümesi hakkında bilgi edinin. Merhaba Pig Latin programlama diline uygulanan toohello giriş veri tooproduce hello istenen çıkış toodescribe dönüşümleri sağlar.

> [!IMPORTANT]
> Merhaba bu belgedeki adımlar Linux tabanlı Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="ssh"></a>SSH ile bağlanma

SSH tooconnect tooyour Hdınsight kümesi kullanın. Merhaba aşağıdaki örnek bağlayan adlı tooa küme **myhdinsight** adlı hello hesabı olarak **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**SSH kimlik doğrulaması için bir sertifika anahtarı sağladıysanız** hello Hdınsight kümesi oluştururken, istemci sisteminizde toospecify hello hello özel anahtarın konumunu gerekebilir.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**SSH kimlik doğrulaması için parola sağladıysanız** hello Hdınsight kümesi oluşturduğunuzda, istendiğinde hello parolasını sağlayın.

Hdınsight ile SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Merhaba Pig komutunu kullanın

1. Bağlantı kurulduktan sonra komutu aşağıdaki hello kullanarak hello Pig komut satırı arabirimi (CLI) başlatın:

        pig

    Bir süre sonra görmelisiniz bir `grunt>` istemi.

2. Aşağıdaki ifadeyi hello girin:

        LOGS = LOAD '/example/data/sample.log';

    Bu komut, oturum AÇTIĞI hello sample.log dosyasının Merhaba içeriğine yükler. Aşağıdaki ifadeyi hello kullanarak hello dosyasının Merhaba içeriğine görüntüleyebilirsiniz:

        DUMP LOGS;

3. Ardından, aşağıdaki ifadeyi hello kullanarak bir normal ifade tooextract yalnızca hello günlük düzeyi her kayıttan uygulayarak hello verileri dönüştürün:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Kullanabileceğiniz **dökümü** tooview hello veri hello dönüştürme sonra. Bu durumda, kullanarak `DUMP LEVELS;`.

4. Aşağıdaki tablonun hello hello deyimleri kullanarak dönüşümleri uygulama devam edin:

    | Pig Latin deyimi | Hangi hello deyimi mu |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Merhaba günlük düzeyi null değerini içeren satırları kaldırır ve hello sonuçları içine depolar `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Grupları hello satırları Günlük düzeyi tarafından ve hello sonuçları içine depolar `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Bir küme oluşturur her benzersiz günlük içeren verilerin düzeyi değeri ve kaç kez oluşur. Merhaba veri kümesi içine depolanır `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Merhaba günlük düzeyleri (Azalan) sayısına göre sıralar ve içine depolar `RESULT`. |

    > [!TIP]
    > Kullanım `DUMP` her adımından sonra hello dönüşümünün tooview hello sonucu.

5. Hello kullanarak bir dönüşüm hello sonuçlarını da kaydedebilirsiniz `STORE` deyimi. Örneğin, aşağıdaki ifadeyi hello hello kaydeder `RESULT` toohello `/example/data/pigout` hello varsayılan depolama kümeniz için dizin:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > Merhaba veri hello adlı dosyaları belirtilen dizinde depolanır `part-nnnnn`. Merhaba dizini zaten varsa, bir hata alırsınız.

6. tooexit hello grunt komut isteminde, aşağıdaki ifadeyi hello girin:

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin toplu iş dosyaları

Merhaba Pig komutu toorun Pig Latin bir dosyada yer alan de kullanabilirsiniz.

1. Merhaba grunt istemi çıktıktan sonra kullanım hello şu komutu toopipe STDIN adlı bir dosyaya `pigbatch.pig`. Bu dosya hello hello SSH kullanıcı hesabı için giriş dizini oluşturulur.

        cat > ~/pigbatch.pig

2. Yazın veya satırlardan hello yapıştırın ve sonra Ctrl + D bittiğinde kullanın.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Kullanım hello şu komutu toorun hello `pigbatch.pig` hello Pig komutunu kullanarak dosya.

        pig ~/pigbatch.pig

    Merhaba toplu işi tamamlandıktan sonra çıktı aşağıdaki hello bakın:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Sonraki adımlar

Hdınsight'ta Pig hakkında genel bilgi için belge aşağıdaki hello bakın:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)

Hdınsight'ta Hadoop ile diğer yolları toowork hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)
