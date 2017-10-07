---
title: "aaaDevelop MapReduce akış Python işleri Hdınsight - Azure | Microsoft Docs"
description: "Bilgi nasıl MapReduce işleri akış Python toouse. Hadoop, Java dışındaki dillerde yazmak için MapReduce için akış bir API sağlar."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>MapReduce programları Hdınsight için akış Python geliştirme

Bilgi nasıl MapReduce işlemleri akış Python toouse. Hadoop, toowrite harita sağlayan ve Java dışındaki dillerde işlevleri azaltmak MapReduce akış bir API sağlar. Merhaba bu belgedeki adımları hello eşleme uygulamak ve Python bileşenlerinde azaltır.

## <a name="prerequisites"></a>Ön koşullar

* Bir Hdınsight kümesinde Linux tabanlı Hadoop

  > [!IMPORTANT]
  > Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Bir metin düzenleyicisi

  > [!IMPORTANT]
  > Merhaba metin düzenleyicisi LF hello satır bitiş olarak kullanmanız gerekir. CRLF satır sonu kullanarak hataları hello MapReduce işi Linux tabanlı Hdınsight kümelerinde çalıştırırken neden olur.

* Merhaba `ssh` ve `scp` komutları veya [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>Sözcük Sayımı

Bu temel sözcük sayımı bir python Eşleyici ve reducer uygulanan bir örnektir. Merhaba Eşleyici cümleleri tek tek sözcüklere böler ve hello reducer hello sözcükler toplar ve tooproduce hello çıkış sayar.

Aşağıdaki akış çizelgesi hello ne hello eşleme sırasında olur ve aşamaları azaltmak gösterilmektedir.

![Merhaba mapreduce işlem çizimi](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>Akış MapReduce

Hadoop toospecify hello eşlemesini içerir ve bir iş tarafından kullanılan mantığı azaltmak bir dosyayı sağlar. hello için belirli gereksinimler Hello harita ve mantığı azaltmak şunlardır:

* **Giriş**: Merhaba eşleme ve azaltma bileşenleri STDIN giriş verilerinin okuma gerekir.
* **Çıktı**: Merhaba eşleme ve azaltma bileşenleri çıkış veri tooSTDOUT yazmanız gerekir.
* **Veri biçimi**: tüketilen ve üretilen hello veri sekmesi karakteriyle ayrılmış bir anahtar/değer çifti olmalıdır.

Python kolayca işleyebilir bu gereksinimleri hello kullanarak `sys` STDIN ve kullanarak modülü tooread `print` tooprint tooSTDOUT. Merhaba kalan görev yalnızca bir sekme hello verilerle biçimlendirme (`\t`) hello anahtar ve değer arasında karakter.

## <a name="create-hello-mapper-and-reducer"></a>Merhaba Eşleyici ve reducer oluşturma

1. Adlı bir dosya oluşturun `mapper.py` ve kullanım hello aşağıdaki kodu hello içerik olarak:

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. Adlı bir dosya oluşturun **reducer.py** ve kullanım hello aşağıdaki kodu hello içerik olarak:

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a>PowerShell kullanarak çalıştırma

PowerShell Betiği aşağıdaki kullanım hello dosyalarınızı hello sağ satır sonları sahip tooensure:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

Aşağıdaki PowerShell komut dosyası tooupload hello dosyaları hello kullanın, hello işini çalıştırın ve hello çıktısını görüntüleyin:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>Bir SSH oturumunda

1. Aynı içinde geliştirme ortamınızdan hello olarak dizin `mapper.py` ve `reducer.py` dosyaları, komut aşağıdaki hello kullanın:

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    Değiştir `username` hello SSH kullanıcı adı, kümeniz için ve `clustername` kümenizin hello ada sahip.

    Bu komut hello yerel sistem toohello baş düğümünden hello dosyalarını kopyalar.

    > [!NOTE]
    > SSH hesabınızın parolası toosecure kullandıysanız, hello parolası istenir. Bir SSH anahtarı kullandıysanız, toouse hello olabilir `-i` parametre ve hello yolu toohello özel anahtarı. Örneğin, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. SSH kullanarak toohello kümesine bağlanın:

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    Daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

3. satır sonları düzeltin, komutları aşağıdaki hello kullan hello tooensure hello mapper.py ve reducer.py vardır:

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. Komut toostart hello MapReduce işi aşağıdaki hello kullanın.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    Bu komut hello aşağıdaki bölümleri içerir:

   * **hadoop streaming.jar**: akış MapReduce işlemleri yaparken kullanılır. Bu Hadoop sağladığınız hello dış MapReduce koduyla arabirimleri.

   * **-dosyaları**: Belirtilen hello ekler dosyaları toohello MapReduce işi.

   * **-Eşleyici**: söyler, toouse Eşleyici hello gibi dosya Hadoop.

   * **-reducer**: söyler, toouse reducer hello gibi dosya Hadoop.

   * **-Giriş**: güvenmemeniz gerekir hello giriş dosyası sözcükleri.

   * **-Çıktı**: çıktı hello hello dizin yazılır.

    Merhaba MapReduce işi çalışıyor gibi hello işlem yüzde olarak görüntülenir.

        02/15/05 19:01:04 bilgisi mapreduce. İş: eşleme %0 azaltmak %0 02/15/05 19:01:16 bilgisi mapreduce. İş: % 0 harita % 100 azaltmak 02/15/05 19:01:27 bilgisi mapreduce. İş: eşleme % %100 100 azaltın.


5. tooview hello çıkışı, komutu aşağıdaki hello kullan:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Bu komut oluştu sözcükleri ve hello word kaç kez listesini görüntüler.

## <a name="next-steps"></a>Sonraki adımlar

Hdınsight ile nasıl MapRedcue akış toouse işleri öğrendiniz, bağlantılar tooexplore aşağıdaki hello Azure Hdınsight ile diğer yolları toowork kullanın.

* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [HDInsight ile MapReduce işleri kullanma](hdinsight-use-mapreduce.md)
