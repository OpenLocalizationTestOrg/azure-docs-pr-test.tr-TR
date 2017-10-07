---
title: "Merhaba sorgu konsol hdınsight'ta - Azure üzerinde Hadoop Hive aaaUse | Microsoft Docs"
description: "Nasıl toouse hello web tabanlı sorgu konsol toorun Hive sorguları bir Hdınsight Hadoop üzerinde tarayıcınızdan küme öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>Merhaba sorgu Konsolu kullanarak Hive sorguları çalıştırma
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Bu makalede, nasıl toouse hello Hdınsight sorgu konsol toorun Hive sorguları bir Hdınsight Hadoop üzerinde tarayıcınızdan küme öğreneceksiniz.

> [!IMPORTANT]
> Merhaba Hdınsight sorgu konsolu yalnızca Windows tabanlı Hdınsight kümelerinde kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Hdınsight 3.4 veya büyük, bkz [Hive sorgularını çalıştırma Ambari Hive görünümünde](hdinsight-hadoop-use-hive-ambari-view.md) bir web tarayıcısından Hive sorguları çalıştırma hakkında bilgi.

## <a id="prereq"></a>Önkoşullar
Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir.

* Windows tabanlı Hdınsight Hadoop kümesi
* Modern bir web tarayıcısı

## <a id="run"></a>Merhaba sorgu Konsolu kullanarak Hive sorguları çalıştırma
1. Bir web tarayıcısı açın ve çok gidin**https://CLUSTERNAME.azurehdinsight.net**, burada **CLUSTERNAME** Hdınsight kümenize hello adıdır. İstenirse, hello kullanıcı adı ve hello küme oluştururken kullandığınız parolayı girin.
2. Merhaba sayfanın üst kısmındaki hello Hello bağlantılardan birini seçin **Hive Düzenleyicisi**. Bu, kullanılan tooenter hello HiveQL ifadelerini toorun hello Hdınsight kümesinde istediğiniz olabilir bir form görüntüler.

    ![Merhaba hive Düzenleyicisi](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    Merhaba metnin yerine `Select * from hivesampletable` aşağıdaki HiveQL ifadelerini hello ile:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

   * **DROP TABLE**: siler hello tablo ve hello veri dosyası hello tablo zaten varsa.
   * **Dış tablo oluştur**: kovanında yeni bir 'external' tablo oluşturur. Dış tablolara yalnızca hello tablo tanımı kovanında depolamak; Merhaba veri hello özgün konumda kalır.

     > [!NOTE]
     > Dış tablolar, bir dış kaynağa (örneğin, bir otomatik veri karşıya yükleme işlemi) veya başka bir MapReduce işlemi tarafından güncelleştirilen veri toobe temel hello beklediğiniz ancak her zaman toouse hello en son verileri Hive sorguları istediğiniz zaman kullanılmalıdır.
     >
     > Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.
     >
     >
   * **SATIR biçimi**: hello veri biçimlendirilmiş nasıl Hive söyler. Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.
   * **AS TEXTFILE konumu DEPOLANAN**: söyler hello veri nerede Hive depolanan (Merhaba örnek/veri dizini) ve metin olarak depolanır
   * **SEÇİN**: tüm satırların sayımını seçin burada sütun **t4** hello değeri içeren **[Hata]**. Bu değeri döndürmelidir **3** çünkü bu değer içeren üç satır vardır.
   * **INPUT__FILE__NAME gibi '%.log'** -biz yalnızca veri biten dosyalarından döndürmelidir Hive söyler. günlük. Merhaba verileri içeren ve verileri diğer örnekten tanımladığımız hello şema eşleşmiyor veri dosyalarını döndürmesini tutar hello arama toohello sample.log dosyası kısıtlar.
3. Tıklatın **gönderme**. Merhaba **proje oturumunu** hello hello sayfanın hello işe yönelik ayrıntıları görüntülenmelidir.
4. Ne zaman hello **durum** değişiklikleri alan çok**tamamlandı**seçin **ayrıntıları görüntüle** hello işi için. Merhaba Ayrıntıları sayfasında hello **iş çıktısı** içeren `[ERROR]    3`. Merhaba kullanabilirsiniz **karşıdan** hello çıktısını hello içeren bir dosyayı bu alan toodownload altında düğmesi.

## <a id="summary"></a>Özet
Gördüğünüz gibi kolay bir yolu toorun sorgu Konsolu sağlar hello Hdınsight kümesinde bir Hive sorguları hello iş durumunu izlemek ve hello çıkış almak.

Hive sorgusu konsol toorun Hive işlerini kullanma hakkında daha fazla toolearn seçin **Başlarken** hello sorgu konsol hello üst kısmında, ardından sağlanan hello örnekleri kullanır. Her örnek Hive tooanalyze verileri hello örnekte kullanılan hello HiveQL ifadelerini hakkında açıklamalar dahil olmak üzere, kullanarak hello işlemi anlatılmaktadır.

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
