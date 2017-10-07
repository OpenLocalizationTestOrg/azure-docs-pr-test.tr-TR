---
title: "Visual Studio - Azure Hdınsight (Hadoop) Data Lake araçları ile aaaHive | Microsoft Docs"
description: "Toouse hello Data Lake Visual Studio toorun için Apache Hive sorguları Azure hdınsight'ta Apache Hadoop ile nasıl araçları hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Merhaba Data Lake araçları için Visual Studio kullanarak Hive sorguları çalıştırma

Visual Studio tooquery için Apache Hive nasıl toouse hello Data Lake araçları hakkında bilgi edinin. Merhaba Data Lake araçları tooeasily izin oluşturma, gönderme ve Azure hdınsight'ta Hive sorguları tooHadoop izleyin.

## <a id="prereq"></a>Önkoşullar

* Azure Hdınsight (Hadoop hdınsight) kümesi

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (sürümleri aşağıdaki hello biri):

    * Visual Studio 2013 Community/Professional/Premium/Ultimate güncelleştirme 4 ile

    * Visual Studio 2015 (herhangi bir sürümünü)

    * Visual Studio 2017 (herhangi bir sürümünü)

* Visual Studio ya da Azure Data Lake araçları Visual Studio için Hdınsight araçları. Bkz: [Hdınsight için Visual Studio Hadoop araçlarını kullanmaya başlamanıza](hdinsight-hadoop-visual-studio-tools-get-started.md) yükleme ve yapılandırma hello araçlar hakkında bilgi için.

## <a id="run"></a>Merhaba Visual Studio kullanarak Hive sorguları çalıştırma

1. Açık **Visual Studio** seçip **yeni** > **proje** > **Azure Data Lake**  >   **HIVE** > **Hive uygulaması**. Bu proje için bir ad sağlayın.

2. Açık hello **Script.hql** bu proje ve aşağıdaki HiveQL ifadelerini hello Yapıştır ile oluşturulan dosyası:

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

   * `DROP TABLE`: Bu bildirimi Hello tablo zaten varsa, onu siler.

   * `CREATE EXTERNAL TABLE`: Yeni bir 'external' tablo kovanında oluşturur. Dış tablolara hello tablo tanımı Hive (Merhaba veri hello özgün konumunda bırakılır) yalnızca depolayın.

     > [!NOTE]
     > Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır. Örneğin, bir MapReduce işi veya Azure hizmeti.
     >
     > Bir dış tablo bırakma mu **değil** hello verileri, yalnızca hello tablo tanımını silin.

   * `ROW FORMAT`: Hello verilerin nasıl biçimlendirilmiş Hive söyler. Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.

   * `STORED AS TEXTFILE LOCATION`: Hive hello burada verilerin depolandığı söyler (Merhaba örnek/veri dizini) ve metin olarak depolanır.

   * `SELECT`: Tüm satırların sayımını seçme Burada sütun `t4` hello değeri içeren `[ERROR]`. Bu ifade değerini döndürür `3` çünkü bu değer içeren üç satır vardır.

   * `INPUT__FILE__NAME LIKE '%.log'`-Hive biz yalnızca veri biten dosyalarından döndürmesi gerektiğini bildirir. günlük. Bu yan tümce hello verileri içeren hello arama toohello sample.log dosyası kısıtlar.

3. Merhaba Hello araç çubuğundan seçin **Hdınsight kümesi** bu sorgu için toouse istiyor. Seçin **gönderme** toorun hello deyimleri Hive işi.

   ![Gönderme çubuğu](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. Merhaba **Hive işi Özet** görünür ve hello işi hakkındaki bilgileri görüntüler. Kullanım hello **yenileme** bağlantı hello kadar toorefresh hello iş bilgileri **iş durumu** çok değiştirir**tamamlandı**.

   ![İş özeti tamamlanmış bir iş görüntüleme](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. Kullanım hello **iş çıktısı** bağlantı bu işin tooview hello çıktı. Görüntülediği `[ERROR] 3`, bu sorgu tarafından döndürülen hello değeri olduğu.

6. Ayrıca, bir proje oluşturmadan Hive sorguları çalıştırabilirsiniz. Kullanarak **Sunucu Gezgini**, genişletin **Azure** > **Hdınsight**Hdınsight sunucunuzun sağ tıklayın ve ardından **Hive sorgusu Yaz** .

7. Merhaba, **temp.hql** görünür, belge aşağıdaki HiveQL ifadelerini hello ekleme:

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

   * `CREATE TABLE IF NOT EXISTS`: Zaten yoksa, bir tablo oluşturur. Çünkü hello `EXTERNAL` anahtar sözcüğü kullanılmaz, bu deyim bir iç tablosu oluşturur. İç tablolar hello Hive veri ambarında depolanır ve Hive tarafından yönetilir.

     > [!NOTE]
     > Farklı `EXTERNAL` tablolar, bir iç tablosu da bırakarak hello alttaki verileri siler.

   * `STORED AS ORC`: En iyi duruma getirilmiş satır sütunlu (ORC) biçimindeki verileri depoları hello. ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.

   * `INSERT OVERWRITE ... SELECT`: Hello satırları seçer `log4jLogs` içeren tablo `[ERROR]`, eklemeleri veri hello hello sonra `errorLogs` tablo.

8. Merhaba araç çubuğundan seçin **gönderme** toorun hello işi. Kullanım hello **iş durumu** toodetermine o hello işi başarıyla tamamlandı.

9. Merhaba tablo, kullanım oluşturulan iş hello tooverify **Sunucu Gezgini** ve genişletin **Azure** > **Hdınsight** > Hdınsight kümenize > **Hive veritabanları** > **varsayılan**. Merhaba **günlüklerini** tablo ve hello **log4jLogs** tablo listelenir.

## <a id="nextsteps"></a>Sonraki adımlar

Gördüğünüz gibi Visual Studio için Hdınsight araçları hello Hdınsight'ta Hive sorguları kolay bir yolu toowork sağlar.

Hdınsight'ta Hive hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)

* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)

Merhaba hakkında daha fazla bilgi için Visual Studio için Hdınsight araçları:

* [Visual Studio için Hdınsight araçlarını kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
