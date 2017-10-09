---
title: "aaaAzure Hdınsight sorun giderme kılavuzları | Microsoft Docs"
description: "Hadoop iş yükleri, Azure Hdınsight kullanarak sorun giderme. Adım adım belgeleri gösterir, nasıl toouse Hdınsight toosolve Hive, Spark, YARN, HBase, HDFS ve Storm ile ortak sorunları."
services: hdinsight
author: arijitt
manager: arijitt
layout: LandingPage
ms.assetid: 
ms.service: hdinsight
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing - page
ms.date: 7/06/2017
ms.author: arijitt
ms.openlocfilehash: 6d801389cba738345b36364302c62008b8318018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-by-using-azure-hdinsight"></a>Azure Hdınsight kullanarak sorun giderme

| Apache iş yükü | Üst sorular |
|---|---|
|![HBase](./media/hdinsight-troubleshoot-guide/HBASE.png)<br>[HBase sorun giderme](hdinsight-troubleshoot-hbase.md)|<br>[Birden çok atanmamış bölgeleri ile nasıl hbck komutu raporları çalıştırılsın mı](hdinsight-troubleshoot-hbase.md#how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions)<br><br>[Zaman aşımı sorunları nasıl hbck komutlarını bölge atamaları kullanırken düzeltme](hdinsight-troubleshoot-hbase.md#how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments)<br><br>[Nasıl ı zorla-HDFS güvenli modda bir kümede devre dışı bırak](hdinsight-troubleshoot-hbase.md#how-do-i-force-disable-hdfs-safe-mode-in-a-cluster)<br><br>[Nasıl JDBC veya SQLLine bağlantısı düzeltirim Apache Phoenix ile ilgili sorunları](hdinsight-troubleshoot-hbase.md#how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix)<br><br>[Ana sunucu toofail toostart nedeni nedir](hdinsight-troubleshoot-hbase.md#what-causes-a-master-server-to-fail-to-start)<br><br>[Bir bölge sunucu üzerinde bir yeniden başlatma hatası nedeni nedir](hdinsight-troubleshoot-hbase.md#what-causes-a-restart-failure-on-a-region-server)|
|![HDFS](./media/hdinsight-troubleshoot-guide/HDFS.png)<br>[HDFS sorun giderme](hdinsight-troubleshoot-hdfs.md)|<br>[Gelen yerel HDFS bir küme içindeki nasıl erişirim](hdinsight-troubleshoot-hdfs.md#how-do-i-access-local-hdfs-from-inside-a-cluster)<br><br>[Nasıl ı zorla-HDFS güvenli modda bir kümede devre dışı bırak](hdinsight-troubleshoot-hdfs.md#how-do-i-force-disable-hdfs-safe-mode-in-a-cluster)|
|![Hive](./media/hdinsight-troubleshoot-guide/HIVE.png)<br>[HBase sorun giderme](hdinsight-troubleshoot-hive.md)|<br>[Nasıl bir Hive meta depo dışarı aktarma ve başka bir kümede alma](hdinsight-troubleshoot-hive.md#how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster)<br><br>[Bir kümede nasıl Hive günlüklerini bulun](hdinsight-troubleshoot-hive.md#how-do-i-locate-hive-logs-on-a-cluster)<br><br>[Merhaba Hive kabuğunu bir kümede belirli yapılandırmalarla nasıl başlatma](hdinsight-troubleshoot-hive.md#how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster)<br><br>[Küme kritik yolunda Tez DAG verileri nasıl çözümlemek](hdinsight-troubleshoot-hive.md#how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path)<br><br>[Bir kümeden nasıl Tez DAG veri karşıdan](hdinsight-troubleshoot-hive.md#how-do-i-download-tez-dag-data-from-a-cluster)|
|![Spark](./media/hdinsight-troubleshoot-guide/SPARK.png)<br>[Spark sorun giderme](hdinsight-troubleshoot-SPARK.md)|<br>[Spark uygulama kümelerinde Ambari kullanarak nasıl yapılandırırım](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-ambari-on-clusters)<br><br>[Spark uygulama kümelerinde Jupyter Not Defteri kullanarak nasıl yapılandırırım](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters)<br><br>[Spark uygulama kümelerinde Livy kullanarak nasıl yapılandırırım](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-livy-on-clusters)<br><br>[Kümelerinde nasıl kullanarak uygulama spark gönderme Spark yapılandırırım](hdinsight-troubleshoot-spark.md#how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters)<br><br>[Ne bir Spark uygulama OutOfMemoryError özel duruma neden olur](hdinsight-troubleshoot-spark.md#what-causes-a-spark-application-outofmemoryerror-exception)|
|![Storm](./media/hdinsight-troubleshoot-guide/STORM.png)<br>[Storm sorun giderme](hdinsight-troubleshoot-STORM.md)|<br>[Bir küme üzerindeki Storm kullanıcı Arabirimi hello nasıl erişirim](hdinsight-troubleshoot-storm.md#how-do-i-access-the-storm-ui-on-a-cluster)<br><br>[Bir topoloji tooanother nasıl Storm olay hub'ı spout denetim noktası bilgilerini Aktarım](hdinsight-troubleshoot-storm.md#how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another)<br><br>[Bir kümede nasıl Storm ikili dosyaları bulun](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-binaries-on-a-cluster)<br><br>[Bir Storm kümesine hello dağıtım topolojisi nasıl belirlerim](hdinsight-troubleshoot-storm.md#how-do-i-determine-the-deployment-topology-of-a-storm-cluster)<br><br>[Geliştirme için Storm olay hub'ı spout ikili dosyalarını nasıl bulun](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-event-hub-spout-binaries-for-development)<br><br>[Storm Log4J yapılandırma dosyalarını kümelerde nasıl bulun](hdinsight-troubleshoot-storm.md#how-do-i-locate-storm-log4j-configuration-files-on-clusters)|
|![YARN](./media/hdinsight-troubleshoot-guide/YARN.png)<br>[YARN sorun giderme](hdinsight-troubleshoot-YARN.md)|<br>[Bir kümede nasıl yeni bir YARN sıra oluşturulsun mu](hdinsight-troubleshoot-yarn.md#how-do-i-create-a-new-yarn-queue-on-a-cluster)<br><br>[Bir kümeden nasıl YARN günlüklerini karşıdan](hdinsight-troubleshoot-yarn.md#how-do-i-download-yarn-logs-from-a-cluster)|

## <a name="hdinsight-troubleshooting-resources"></a>Hdınsight sorun giderme kaynakları

| Hakkında bilgi için | Bu makalelere bakın |
| --- | --- |
| Hdınsight Linux ve en iyi duruma getirme | - [Linux'ta Hdınsight kullanma hakkında bilgi](hdinsight-hadoop-linux-information.md)<br>- [Hadoop bellek ve performans sorunlarını giderme](hdinsight-hadoop-stack-trace-error-messages.md)<br>- [Hive sorgu performansı](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/) |
| Günlükleri ve dökümleri | - [Linux üzerinde erişim Hadoop YARN uygulama günlükleri](hdinsight-hadoop-access-yarn-app-logs-linux.md)<br>- [Linux'ta Hadoop Hizmetleri için yığın dökümleri etkinleştir](hdinsight-hadoop-collect-debug-heap-dump-linux.md)<br>- [Hdınsight günlüklerini analiz edin](hdinsight-debug-jobs.md)|
| Hatalar | - [Anlama ve WebHCat hatalarını çözümleme](hdinsight-hadoop-templeton-webhcat-debug-errors.md)<br>- [Ayarları toofix OutofMemory hata yığını](hdinsight-hadoop-hive-out-of-memory-error-oom.md) |
| Araçlar | - [Ambari görünümleri toodebug Tez işlerinde kullanın](hdinsight-debug-ambari-tez-view.md)<br>- [Hive sorguları en iyi duruma getirme](hdinsight-hadoop-optimize-hive-query.md) |
