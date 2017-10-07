---
title: "hdınsight'ta - Azure Hadoop Hizmetleri tarafından kullanılan aaaPorts | Microsoft Docs"
description: "Hdınsight üzerinde çalışan Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları listesi."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları

Bu belge Linux tabanlı Hdınsight kümelerinde çalışan Hadoop Hizmetleri tarafından kullanılan hello bağlantı noktalarının bir listesini sağlar. Ayrıca, bağlantı noktaları hakkında bilgi SSH kullanarak tooconnect toohello küme kullanılan sağlar.

## <a name="public-ports-vs-non-public-ports"></a>Genel olmayan bağlantı noktaları ve ortak bağlantı noktaları

Linux tabanlı Hdınsight kümeleri yalnızca üç bağlantı noktalarını herkese açık şekilde üzerinde kullanıma Internet hello; 22, 23 ve 443'tür. Bu bağlantı noktaları SSH ve hello güvenli HTTPS protokolü üzerinden kullanıma sunulan hizmetler kullanarak kullanılan toosecurely erişim hello kümelerdir.

Hdınsight tarafından birden fazla Azure sanal makineleri (Merhaba küme içindeki düğümler hello) dahili olarak uygulanan bir Azure sanal ağ üzerinde çalışıyor. Merhaba sanal ağ içinde bağlantı noktaları hello gösterilmeyen erişebilirsiniz Internet. SSH kullanarak hello baş düğümler tooone bağlanıyorsanız, örneğin, hello baş düğümünden sonra doğrudan hello küme düğümleri üzerinde çalışan hizmetleri erişebilirsiniz.

> [!IMPORTANT]
> Hdınsight için bir yapılandırma seçeneği olarak bir Azure sanal ağı belirtmezseniz otomatik olarak oluşturulur. Ancak, diğer makinelere (örneğin, diğer Azure sanal makineler veya istemci geliştirme makinenizdeki) toothis sanal ağ katılamaz.


toojoin ek makineleri toohello sanal ağ, ilk hello sanal ağ oluşturun ve ardından, Hdınsight kümesi oluştururken belirtmeniz gerekir. Daha fazla bilgi için bkz: [bir Azure sanal ağı kullanarak Hdınsight genişletme özellikleri](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>Ortak bağlantı noktaları

Bir Hdınsight küme düğümlerinde bir Azure sanal ağında bulunan ve gelen doğrudan erişilemez tüm hello Internet hello. Ortak ağ geçidi tüm Hdınsight küme türleri arasında ortak olan bağlantı noktaları aşağıdaki internet erişimi toohello sağlar.

| Hizmet | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |İstemcileri toosshd hello birincil headnode üzerinde bağlanır. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |22 |SSH |Merhaba kenar düğümü üzerindeki istemcileri toosshd bağlanır. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |23 |SSH |İstemcileri toosshd hello ikincil headnode üzerinde bağlanır. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md). |
| Ambari |443 |HTTPS |Ambari web kullanıcı Arabirimi. Bkz: [hello Ambari Web kullanıcı arabirimini yönetmek Hdınsight kullanma](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |Ambari REST API. Bkz: [hello Ambari REST API yönetmek Hdınsight kullanma](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |HCatalog REST API. Bkz: [Curl ile Hive kullanma](hdinsight-hadoop-use-pig-curl.md), [Curl ile Pig kullanma](hdinsight-hadoop-use-pig-curl.md), [Curl ile MapReduce kullanma](hdinsight-hadoop-use-mapreduce-curl.md) |
| HiveServer2 |443 |ODBC |ODBC kullanarak tooHive bağlanır. Bkz: [hello Microsoft ODBC sürücüsü ile bağlanma Excel tooHDInsight](hdinsight-connect-excel-hive-odbc-driver.md). |
| HiveServer2 |443 |JDBC |TooHive JDBC kullanarak bağlanır. Bkz: [tooHive hello Hive JDBC sürücüsü kullanarak hdınsight'ta Bağlan](hdinsight-connect-hive-jdbc-driver.md) |

Merhaba aşağıdaki belirli küme türleri için kullanılabilir:

| Hizmet | Bağlantı noktası | Protokol | Küme türü | Açıklama |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |HBase REST API. Bkz: [HBase kullanmaya başlama](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |Spark REST API. Bkz: [uzaktan Livy kullanarak Spark gönderme işleri](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |Storm web kullanıcı Arabirimi. Bkz: [dağıtma ve Hdınsight üzerinde Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>Kimlik Doğrulaması

Genel olarak Internet SSO'yu hello üzerinde gösterilen tüm hizmetler:

| Bağlantı noktası | Kimlik Bilgileri |
| --- | --- |
| 22 veya 23 |Küme oluşturma sırasında belirtilen hello SSH kullanıcı kimlik |
| 443 |Merhaba oturum açma adı (varsayılan: Yönetici) ve küme oluşturma sırasında ayarlanan parola |

## <a name="non-public-ports"></a>Ortak olmayan bağlantı noktaları

> [!NOTE]
> Bazı hizmetler, yalnızca belirli küme türlerinde kullanılabilir. Örneğin, HBase yalnızca HBase kümesi türlerinde kullanılabilir.

> [!IMPORTANT]
> Bazı hizmetler, aynı anda yalnızca bir headnode üzerinde çalıştırın. Merhaba birincil headnode tooconnect toohello hizmeti denemek ve 404 hatası alırsanız hello ikincil headnode kullanarak yeniden deneyin.

### <a name="ambari"></a>Ambari

| Hizmet | Düğümler | Bağlantı noktası | URL yolu | Protokol | 
| --- | --- | --- | --- | --- |
| Ambari web kullanıcı Arabirimi | Baş düğümler | 8080 | / | HTTP |
| Ambari REST API | Baş düğümler | 8080 | / api/v1 | HTTP |

Örnekler:

* Ambari REST API:`curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>HDFS bağlantı noktaları

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| İş web kullanıcı Arabirimi |Baş düğümler |30070 |HTTPS |Web kullanıcı Arabirimi tooview durumu |
| İş meta veri hizmeti |Baş düğümler |8020 |IPC |Dosya sistemi meta verileri |
| DataNode |Tüm çalışan düğümleri |30075 |HTTPS |Web kullanıcı Arabirimi tooview durumu, günlükleri, vb. |
| DataNode |Tüm çalışan düğümleri |30010 |&nbsp; |Veri aktarımı |
| DataNode |Tüm çalışan düğümleri |30020 |IPC |Meta veri işlemleri |
| İkincil iş |Baş düğümler |50090 |HTTP |İş meta veriler için denetim noktası |

### <a name="yarn-ports"></a>YARN bağlantı noktaları

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| Resource Manager web kullanıcı Arabirimi |Baş düğümler |8088 |HTTP |Web kullanıcı Arabirimi için kaynak yöneticisi |
| Resource Manager web kullanıcı Arabirimi |Baş düğümler |8090 |HTTPS |Web kullanıcı Arabirimi için kaynak yöneticisi |
| Kaynak Yöneticisi'ni yönetim arabirimi |Baş düğümler |8141 |IPC |Uygulama gönderimleri için (Hive, Pig, Hive sunucu vs.) |
| Kaynak Manager Zamanlayıcısı |Baş düğümler |8030 |HTTP |Yönetim Arabirimi |
| Kaynak Yöneticisi uygulama arabirimi |Baş düğümler |8050 |HTTP |Merhaba uygulamaları Yöneticisi arabirimi adresidir |
| NodeManager |Tüm çalışan düğümleri |30050 |&nbsp; |Merhaba kapsayıcı Yöneticisi Hello adresidir |
| NodeManager web kullanıcı Arabirimi |Tüm çalışan düğümleri |30060 |HTTP |Kaynak Yöneticisi arabirimi |
| Zaman Çizelgesi adresi |Baş düğümler |10200 |RPC |Merhaba zaman çizelgesi RPC hizmeti. |
| Zaman Çizelgesi web kullanıcı Arabirimi |Baş düğümler |8181 |HTTP |Merhaba zaman çizelgesi hizmet web kullanıcı Arabirimi |

### <a name="hive-ports"></a>Hive bağlantı noktaları

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| HiveServer2 |Baş düğümler |10001 |Thrift |Hizmet tooHive (Thrift/JDBC) bağlamak için |
| Hive meta depo |Baş düğümler |9083 |Thrift |Hizmet bağlantı tooHive meta veriler (Thrift/JDBC) için |

### <a name="webhcat-ports"></a>WebHCat bağlantı noktaları

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| WebHCat sunucu |Baş düğümler |30111 |HTTP |Web API üstünde HCatalog ve diğer Hadoop Hizmetleri |

### <a name="mapreduce-ports"></a>MapReduce bağlantı noktaları

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| Kaynak |Baş düğümler |19888 |HTTP |MapReduce kaynak web kullanıcı Arabirimi |
| Kaynak |Baş düğümler |10020 |&nbsp; |MapReduce kaynak sunucusu |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |Toorequesting Reducers aktarımları Ara harita çıkarır |

### <a name="oozie"></a>Oozie

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| Oozie sunucu |Baş düğümler |11000 |HTTP |Oozie hizmeti URL'si |
| Oozie sunucu |Baş düğümler |11001 |HTTP |Oozie Yönetim için bağlantı noktası |

### <a name="ambari-metrics"></a>Ambari ölçümleri

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| Zaman Çizelgesi (uygulama geçmişi) |Baş düğümler |6188 |HTTP |Merhaba zaman çizelgesi hizmet web kullanıcı Arabirimi |
| Zaman Çizelgesi (uygulama geçmişi) |Baş düğümler |30200 |RPC |Merhaba zaman çizelgesi hizmet web kullanıcı Arabirimi |

### <a name="hbase-ports"></a>HBase bağlantı noktaları

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| HMaster |Baş düğümler |16000 |&nbsp; |&nbsp; |
| HMaster bilgisi Web kullanıcı Arabirimi |Baş düğümler |16010 |HTTP |Merhaba HBase ana web kullanıcı Arabirimi için başlangıç bağlantı noktası |
| Bölge sunucu |Tüm çalışan düğümleri |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |istemcilerin tooconnect tooZooKeeper kullanmasını hello bağlantı noktası |

### <a name="kafka-ports"></a>Kafka bağlantı noktaları

| Hizmet | Düğümler | Bağlantı noktası | Protokol | Açıklama |
| --- | --- | --- | --- | --- |
| Aracısı |Çalışan düğümü |9092 |[Kafka kablo protokolü](http://kafka.apache.org/protocol.html) |İstemci iletişimi için kullanılan |
| &nbsp; |Zookeeper düğümleri |2181 |&nbsp; |istemcilerin tooconnect tooZookeeper kullanmasını hello bağlantı noktası |

### <a name="spark-ports"></a>Spark bağlantı noktaları

| Hizmet | Düğümler | Bağlantı noktası | Protokol | URL yolu | Açıklama |
| --- | --- | --- | --- | --- | --- |
| Spark Thrift sunucuları |Baş düğümler |10002 |Thrift | &nbsp; | Hizmet tooSpark SQL (Thrift/JDBC) bağlamak için |
| Livy sunucu | Baş düğümler | 8998 | HTTP | /batches | Deyimler, işleri ve uygulamaları çalıştırmak için hizmeti |

Örnekler:

* Livy: `curl "http://10.0.0.11:8998/batches"`. Bu örnekte, `10.0.0.11` hello Livy hizmeti barındıran hello headnode hello IP adresidir.
