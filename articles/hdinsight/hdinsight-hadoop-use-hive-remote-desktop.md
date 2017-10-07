---
title: "aaaUse Hadoop Hive ve Hdınsight - Azure de Uzak Masaüstü | Microsoft Docs"
description: "Nasıl tooconnect tooHadoop küme Hdınsight'ta Uzak Masaüstü'nü kullanarak öğrenin ve Hive sorguları hello Hive komut satırı arabirimi kullanarak çalıştırın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Uzak Masaüstü kullanarak hdınsight'ta Hadoop ile Hive kullanma
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Bu makalede, Hdınsight Uzak Masaüstü'nü kullanarak küme ve Hive çalıştırmak tooconnect tooan hello Hive komut satırı arabirimi (CLI) kullanarak nasıl sorgular öğreneceksiniz.

> [!IMPORTANT]
> Uzak Masaüstü, Windows hello işletim sistemi olarak kullanma Hdınsight kümelerinde yalnızca kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Hdınsight 3.4 veya büyük, bkz [Hdınsight ve Beeline ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md) Hive sorguları doğrudan hello kümede bir komut satırından çalıştırma hakkında bilgi.

## <a id="prereq"></a>Önkoşullar
Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir:

* Bir Windows tabanlı Hdınsight (Hadoop hdınsight) kümesi
* Windows 10, Windows 8 veya Windows 7 çalıştıran bir istemci bilgisayar

## <a id="connect"></a>İle Uzak Masaüstü Bağlantısı
Merhaba Hdınsight kümesi için Uzak Masaüstü'nü etkinleştirin, ardından hello yönergeleri izleyerek tooit bağlayın [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Merhaba Hive komutunu kullanın
Merhaba Hdınsight kümesi için toohello Masaüstü bağlıyken adımları toowork Hive ile aşağıdaki hello kullanın:

1. Merhaba Hello Hdınsight masaüstünden başlatmak **Hadoop komut satırı**.
2. Komut toostart hello Hive CLI aşağıdaki hello girin:

        %hive_home%\bin\hive

    Merhaba CLI başlatıldığında göreceğiniz hello Hive CLI istemi: `hive>`.
3. Merhaba, CLI kullanarak girin deyimleri toocreate adlı yeni bir tablo aşağıdaki hello **log4jLogs** örnek verileri kullanarak:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

   * **DROP TABLE**: siler hello tablo ve hello veri dosyası hello tablo zaten varsa.
   * **Dış tablo oluştur**: kovanında yeni bir 'external' tablo oluşturur. Dış tablolara yalnızca hello tablo tanımı Hive (Merhaba veri hello özgün konumunda bırakılır) depolayın.

     > [!NOTE]
     > Dış tablolar, bir dış kaynağa (örneğin, bir otomatik veri karşıya yükleme işlemi) veya başka bir MapReduce işlemi tarafından güncelleştirilen veri toobe temel hello beklediğiniz ancak her zaman toouse hello en son verileri Hive sorguları istediğiniz zaman kullanılmalıdır.
     >
     > Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.
     >
     >
   * **SATIR biçimi**: hello veri biçimlendirilmiş nasıl Hive söyler. Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.
   * **AS TEXTFILE konumu DEPOLANAN**: söyler hello veri nerede Hive depolanan (Merhaba örnek/veri dizini) ve metin olarak depolanır.
   * **SEÇİN**: tüm satırların sayımını seçer Burada sütun **t4** hello değeri içeren **[Hata]**. Bu değeri döndürmelidir **3** çünkü bu değer içeren üç satır vardır.
   * **INPUT__FILE__NAME gibi '%.log'** -biz yalnızca veri biten dosyalarından döndürmelidir Hive söyler. günlük. Merhaba verileri içeren ve verileri diğer örnekten tanımladığımız hello şema eşleşmiyor veri dosyalarını döndürmesini tutar hello arama toohello sample.log dosyası kısıtlar.
4. Aşağıdaki deyimleri toocreate adlı yeni bir 'iç' tablo kullanım hello **günlüklerini**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

   * **Tablo IF değil var oluşturmak**: zaten yoksa, bir tablo oluşturur. Çünkü hello **dış** anahtar sözcüğü kullanılmaz, hello Hive veri ambarında depolanır ve Hive tamamen yönetilen bir iç tablosu budur.

     > [!NOTE]
     > Farklı **dış** tablolar, bir iç tablosu da bırakarak hello alttaki verileri siler.
     >
     >
   * **AS ORC DEPOLANAN**: en iyi duruma getirilmiş satır sütun (ORC) biçiminde hello verileri depolar. Kovan verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimde budur.
   * **INSERT ÜZERİNE... SEÇİN**: hello satırları seçer **log4jLogs** içeren tablo **[Hata]**, eklemeleri veri hello hello sonra **günlüklerini** tablo.

     yalnızca, satırları tooverify içeren **[Hata]** sütun t4 saklı toohello olan **günlüklerini** tablo, tüm satırları hello deyimi tooreturn aşağıdaki hello kullan **günlüklerini**:

       SEÇİN * günlüklerini; gelen

     Üç veri satırı döndürülmesi, tüm içeren **[Hata]** sütun t4 içinde.

## <a id="summary"></a>Özet
Gördüğünüz gibi hello hello Hive komutu Hive sorguları bir Hdınsight kümesi üzerinde çalışan bir kolay bir yolu toointeractively sağlar, İzleyicisi Merhaba durumu iş ve hello çıkış almak.

## <a id="nextsteps"></a>Sonraki adımlar
Hdınsight'ta Hive hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)

Tez Hive ile kullanıyorsanız, belgeleri hata ayıklama bilgileri için aşağıdaki hello bakın:

* [Windows tabanlı Hdınsight üzerinde Hello Tez UI kullanın](hdinsight-debug-tez-ui.md)
* [Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
