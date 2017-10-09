---
title: "aaaMapReduce ve hdınsight'ta - Azure Hadoop ile SSH bağlantısı | Microsoft Docs"
description: "Hdınsight'ta Hadoop kullanarak nasıl toouse SSH toorun MapReduce işleri öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>Hdınsight ile SSH Hadoop ile MapReduce kullanma

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Nasıl bir güvenli Kabuk (SSH) bağlantısı tooHDInsight toosubmit MapReduce işleri öğrenin.

> [!NOTE]
> Zaten biliyorsanız Linux tabanlı Hadoop kullanmaya sunucuları, ancak yeni tooHDInsight bkz [Linux tabanlı Hdınsight ipuçları](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Önkoşullar

* Linux tabanlı Hdınsight (Hadoop hdınsight) küme

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Bir SSH istemcisi. Daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a id="ssh"></a>SSH ile bağlanma

SSH kullanarak toohello kümesine bağlanın. Örneğin, komutu aşağıdaki hello adlı tooa küme bağlayan **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**SSH kimlik doğrulaması için bir sertifika anahtarı kullanırsanız**, örneğin, istemci sisteminizde toospecify hello hello özel anahtarın konumunu gerekebilir:

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**SSH kimlik doğrulaması için bir parola kullanıyorsanız**, istendiğinde tooprovide hello parolası gerekir.

Hdınsight ile SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Hadoop komutları kullanın

1. Bağlı toohello Hdınsight kümesi olduktan sonra komutu toostart bir MapReduce işi aşağıdaki hello kullan:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    Bu komut hello başlatır `wordcount` hello bulunan sınıfı `hadoop-mapreduce-examples.jar` dosya. Merhaba kullanan `/example/data/gutenberg/davinci.txt` belge giriş ve çıkış olarak depolandı `/example/data/WordCountOutput`.

    > [!NOTE]
    > Bu MapReduce işi ve hello örnek veriler hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop içinde kullanım MapReduce](hdinsight-use-mapreduce.md).

2. Merhaba iş, işler ve metin hello işi tamamlandığında aşağıdaki bilgileri benzer toohello döndürür Ayrıntılar gösterir:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Merhaba işi tamamlandığında, aşağıdaki komut toolist hello çıktı dosyaları hello kullan:

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    Bu komut, iki dosya görüntülemek `_SUCCESS` ve `part-r-00000`. Merhaba `part-r-00000` dosyası hello çıktı bu iş için içerir.

    > [!NOTE]
    > Bazı MapReduce işleri hello sonuçları birden çok bölme **bölümü r ###** dosyaları. Öyleyse, hello kullan ### soneki hello dosyalarının tooindicate hello sırası.

4. tooview hello çıkışı, komutu aşağıdaki hello kullan:

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    Bu komut hello içerdiği hello sözcüklerin listesini görüntüler **wasb://example/data/gutenberg/davinci.txt** dosya ve hello sayısı her sözcüğün oluştu. Merhaba aşağıdaki metni hello dosyasında yer alan hello veri örneğidir:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Özet

Gördüğünüz gibi Hadoop komutları bir Hdınsight kümesi ve sonra Görünüm hello iş çıktısı MapReduce işleri kolay bir yolu toorun sağlar.

## <a id="nextsteps"></a>Sonraki adımlar

Hdınsight'ta MapReduce işleri hakkında genel bilgi için:

* [Hdınsight Hadoop MapReduce kullanın](hdinsight-use-mapreduce.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
