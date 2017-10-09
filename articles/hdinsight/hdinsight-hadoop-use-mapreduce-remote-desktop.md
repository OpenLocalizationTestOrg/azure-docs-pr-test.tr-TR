---
title: "aaaMapReduce ve hdınsight'ta - Azure Hadoop ile Uzak Masaüstü | Microsoft Docs"
description: "Bilgi nasıl toouse Uzak Masaüstü tooconnect tooHadoop Hdınsight ve çalışma MapReduce işleri."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>Uzak Masaüstü kullanarak hdınsight'ta Hadoop MapReduce kullanın
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Bu makalede, nasıl tooconnect tooa hdınsight'ta Hadoop küme Uzak Masaüstü'nü kullanarak öğrenin ve MapReduce işleri hello Hadoop komutunu kullanarak çalıştırın.

> [!IMPORTANT]
> Uzak Masaüstü yalnızca Windows tabanlı Hdınsight kümelerinde kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Hdınsight 3.4 veya büyük, bkz [SSH ile kullanım MapReduce](hdinsight-hadoop-use-mapreduce-ssh.md) toohello Hdınsight kümesine bağlanma ve MapReduce işleri çalıştırma hakkında bilgi için.

## <a id="prereq"></a>Önkoşullar
Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir:

* Bir Windows tabanlı Hdınsight (Hadoop hdınsight) kümesi
* Windows 10, Windows 8 veya Windows 7 çalıştıran bir istemci bilgisayar

## <a id="connect"></a>İle Uzak Masaüstü Bağlantısı
Merhaba Hdınsight kümesi için Uzak Masaüstü'nü etkinleştirin, ardından hello yönergeleri izleyerek tooit bağlayın [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hadoop"></a>Merhaba Hadoop komutunu kullanın
Merhaba Hdınsight kümesi için bağlı toohello Masaüstü olduğunda hello Hadoop komutunu kullanarak adımları toorun bir MapReduce işi aşağıdaki hello kullanın:

1. Merhaba Hello Hdınsight masaüstünden başlatmak **Hadoop komut satırı**. Bu yeni bir komut istemi hello açar **c:\apps\dist\hadoop-&lt;sürüm numarası >** dizin.

   > [!NOTE]
   > Hadoop güncelleştirildikçe hello sürüm numarasını değiştirir. Merhaba **HADOOP_HOME** ortam değişkeni kullanılan toofind hello yolu olabilir. Örneğin, `cd %HADOOP_HOME%` tooknow hello sürüm numarası gerektirmeden değişiklikleri dizinleri toohello Hadoop dizini.
   >
   >
2. toouse hello **Hadoop** komut toorun bir örnek MapReduce işi, hello aşağıdaki komutu kullanın:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Bu hello başlatır **wordcount** hello bulunan sınıfı **hadoop mapreduce examples.jar** hello geçerli dizinde dosya. İsteğe bağlı olarak giriş olarak hello kullanır **wasb://example/data/gutenberg/davinci.txt** belge ve çıktı konumunda depolanır: **wasb: / / / örnek/data/WordCountOutput**.

   > [!NOTE]
   > Bu MapReduce işi ve hello örnek veriler hakkında daha fazla bilgi için bkz: <a href="hdinsight-use-mapreduce.md">Hdınsight Hadoop içinde kullanım MapReduce</a>.
   >
   >
3. Merhaba iş ayrıntıları bu işlenir ve hello iş tamamlandığında bilgi benzer toohello aşağıdaki döndürür gösterir:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. Hello iş tamamlandıktan sonra aşağıdaki komut toolist hello çıktı dosyaları depolandığı hello kullanmak **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    Bu iki dosya görüntülenmelidir **_SUCCESS** ve **bölümü r 00000**. Merhaba **bölümü r 00000** dosyası hello çıktı bu iş için içerir.

   > [!NOTE]
   > Bazı MapReduce işleri hello sonuçları birden çok bölme **bölümü r ###** dosyaları. Öyleyse, hello kullan ### soneki hello dosyalarının tooindicate hello sırası.
   >
   >
5. tooview hello çıkışı, komutu aşağıdaki hello kullan:

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    Bu hello içerdiği hello sözcüklerin listesini görüntüler **wasb://example/data/gutenberg/davinci.txt** hello her sözcüğün yapma sayısı yanı sıra dosya. Merhaba, hello dosyasında yer alan hello veri örneği aşağıdadır:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Özet
Gördüğünüz gibi hello Hadoop komutu kolay bir yolu toorun MapReduce işleri bir Hdınsight kümesi ve görünüm hello iş çıktısı sonra sağlar.

## <a id="nextsteps"></a>Sonraki adımlar
Hdınsight'ta MapReduce işleri hakkında genel bilgi için:

* [Hdınsight Hadoop MapReduce kullanın](hdinsight-use-mapreduce.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
