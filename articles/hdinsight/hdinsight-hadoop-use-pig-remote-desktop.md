---
title: "aaaUse hdınsight'ta - Azure Uzak Masaüstü ile Hadoop Pig | Microsoft Docs"
description: "Nasıl toouse hello Pig komutu toorun Pig Latin deyimleri kümeden bir Uzak Masaüstü Bağlantısı tooa Windows tabanlı Hadoop hdınsight'ta öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>Uzak Masaüstü bağlantısı üzerinden pig işleri çalıştırma
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Bu belge, bir Uzak Masaüstü Bağlantısı tooa Windows tabanlı Hdınsight kümeden hello Pig komutu toorun Pig Latin deyimleri kullanmak için bir kılavuz sağlar. Pig Latin veri dönüşümleri açıklayarak toocreate MapReduce uygulamaların sağlayan yerine harita ve işlevleri azaltır.

> [!IMPORTANT]
> Uzak Masaüstü, Windows hello işletim sistemi olarak kullanma Hdınsight kümelerinde yalnızca kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Hdınsight 3.4 veya büyük, bkz [Hdınsight ve SSH ile Pig kullanma](hdinsight-hadoop-use-pig-ssh.md) etkileşimli olarak Pig çalıştırma hakkında bilgi için doğrudan hello işlerine bir komut satırı ile küme.

## <a id="prereq"></a>Önkoşullar
Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir.

* Bir Windows tabanlı Hdınsight (Hadoop hdınsight) kümesi
* Windows 10, Windows 8 veya Windows 7 çalıştıran bir istemci bilgisayar

## <a id="connect"></a>İle Uzak Masaüstü Bağlantısı
Merhaba Hdınsight kümesi için Uzak Masaüstü'nü etkinleştirin, ardından hello yönergeleri izleyerek tooit bağlayın [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="pig"></a>Merhaba Pig komutunu kullanın
1. Uzak Masaüstü bağlantı kurduktan sonra hello Başlat **Hadoop komut satırı** hello masaüstünde hello simgesini kullanarak.
2. Toostart hello Pig komutu aşağıdaki hello kullan:

        %pig_home%\bin\pig

    İle sunulur bir `grunt>` istemi.
3. Aşağıdaki ifadeyi hello girin:

        LOGS = LOAD 'wasb:///example/data/sample.log';

    Bu komut hello sample.log dosyasının Merhaba içeriğine hello GÜNLÜKLERİ dosyasına yükler. Merhaba dosyasının Merhaba içeriğine komutu aşağıdaki hello kullanarak görüntüleyebilirsiniz:

        DUMP LOGS;
4. Merhaba verileri her kaydından bir normal ifade tooextract yalnızca hello günlük düzeyi uygulayarak dönüştürün:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Kullanabileceğiniz **dökümü** tooview hello veri hello dönüştürme sonra. Bu durumda, `DUMP LEVELS;`.
5. Deyimlerini aşağıdaki hello kullanarak dönüşümleri uygulama devam edin. Kullanım `DUMP` her adımından sonra hello dönüşümünün tooview hello sonucu.

    <table>
    <tr>
    <th>Deyimi</th><th>Neler yapar?</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = LOGLEVEL FİLTRE DÜZEYLERİYLE null; değil</td><td>Merhaba günlük düzeyi null değerini içeren satırları kaldırır ve hello sonuçları FILTEREDLEVELS depolar.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS Grup FILTEREDLEVELS LOGLEVEL tarafından; =</td><td>Grupları hello günlük düzeyi tarafından satırlar ve hello sonuçları GROUPEDLEVELS depolar.</td>
    </tr>
    <tr>
    <td>Sıklık foreach = GROUPEDLEVELS sayısı (FILTEREDLEVELS LOGLEVEL Grup Oluştur. LOGLEVEL) sayısı gibi;</td><td>Yeni bir küme oluşturur her benzersiz günlük içeren verilerin düzeyi değeri ve kaç kez oluşur. Bu SIKLIKLARINI depolanır</td>
    </tr>
    <tr>
    <td>Sonuç order SIKLIĞI sayısı desc tarafından; =</td><td>Merhaba günlük düzeyleri (Azalan) sayısı ve depoları sonucu sıralar</td>
    </tr>
    </table>
6.Hello kullanarak bir dönüşüm hello sonuçlarını da kaydedebilirsiniz `STORE` deyimi. Örneğin, komutu aşağıdaki hello hello kaydeder `RESULT` toohello **/example/data/pigout** kümenizin hello varsayılan depolama kapsayıcısını dizin:

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > Merhaba veri hello adlı dosyaları belirtilen dizinde depolanır **bölümü nnnnn**. Merhaba dizini zaten varsa, bir hata iletisi alırsınız.
   >
   >
7. tooexit hello grunt komut isteminde, aşağıdaki ifadeyi hello girin.

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin toplu iş dosyaları
Bir dosyada hello Pig komutu toorun yer Pig Latin de kullanabilirsiniz.

1. Merhaba grunt istemi çıktıktan sonra açmak **not defteri** ve adlı yeni bir dosya oluşturun **pigbatch.pig** hello içinde **PIG_HOME %** dizin.
2. Türü veya Yapıştır hello aşağıdaki satırları hello **pigbatch.pig** dosya ve dosyayı kaydedin:

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. Kullanım hello toorun hello aşağıdaki **pigbatch.pig** hello pig komutunu kullanarak dosya.

        pig %PIG_HOME%\pigbatch.pig

    Merhaba toplu işi tamamlandığında aynı olarak kullanıldığında hello çıktı aşağıdaki hello görmelisiniz `DUMP RESULT;` hello önceki adımlarda:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>Özet
Gördüğünüz gibi hello Pig komutu, MapReduce işlemleri çalıştırın ya da bir toplu iş dosyasında depolanan Pig Latin işleri çalıştırma toointeractively sağlar.

## <a id="nextsteps"></a>Sonraki adımlar
Hdınsight'ta Pig hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)
