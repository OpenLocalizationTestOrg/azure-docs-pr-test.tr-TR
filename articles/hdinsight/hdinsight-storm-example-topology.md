---
title: "Hdınsight üzerinde Apache Storm topolojilerini aaaExample | Microsoft Docs"
description: "Örnek Storm topolojileri listesi oluşturulur ve olay hub'larıyla çalışma ve temel C# ve Java topolojileri dahil olmak üzere Hdınsight üzerinde Apache Storm ile test."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Örnek Storm topolojileri ve Hdınsight üzerinde Apache Storm bileşenleri

Merhaba, oluşturulur ve Hdınsight üzerinde Apache Storm ile kullanılmak üzere Microsoft tarafından yönetilen örnekleri listesi verilmiştir. Bu örnekler, olay hub'ları, Cosmos DB, Power BI, SQL Database, Hdınsight ve Azure Storage HBase gibi Azure hizmetleriyle temel C# ve Java topolojileri tooworking oluşturmasına konular, çeşitli kapsar. Ayrıca bazı örnekler göstermektedir nasıl toowork SignalR ve Socket.IO gibi Azure olmayan veya hatta Microsoft dışı teknolojileri ile.

| Açıklama | Gösterir | Dil/Framework |
|:--- |:--- |:--- |
| [Apache Storm tooAzure Data Lake Store yazma](hdinsight-storm-write-data-lake-store.md) |TooAzure Data Lake Store yazma |Java |
| [Event Hubs Spout ve Cıvata kaynağı](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Merhaba Event Hubs Spout ve Cıvata için kaynağı |Java |
| [Hdınsight üzerinde Apache Storm için Java tabanlı topolojiler geliştirme][5797064f] |Maven |Java |
| [Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme][16fce2d1] |Visual Studio için HDInsight Araçları |C#, Java |
| [Bir C# Storm topolojisinde birden çok veri akışı oluşturma][ec5a4064] |Birden çok akış |C# |
| [Azure Event hubs'tan (C#) hdınsight'ta Storm işlem olayları][844d1d81] |Event Hubs |C# ve Java |
| [Azure Event hubs'tan (Java) hdınsight'ta Storm işlem olayları](hdinsight-storm-develop-java-event-hub-topology.md) |Event Hubs |Java |
| [Power BI toovisualize veri bir Storm topolojisinin kullanın][94d15238] |Power BI |C# |
| [Storm ve hdınsight'ta HBase ile sensör verilerini analiz etme][ab894747] |Olay hub'ları, HBase, Socket.IO, Web Panosu |C#, Java, JavaScript, HTML |
| [Event Hubs Hdınsight üzerinde Storm kullanmaya aracın algılayıcı verilerini işlemek][246ee964] |Olay hub'ları, Cosmos DB Azure depolama blobunu (WASB) |C#, Java |
| [Ayıklama, dönüştürme ve yükleme (Hdınsight üzerinde Storm kullanmaya ETL) Azure Event Hubs tooHBase gelen][b4b68194] |Olay hub'ları, HBase |C# |
| [Hdınsight üzerinde Storm Azure hizmetlerinden ile çalışmak için şablon C# Storm topolojisini proje][ce0c02a2] |Olay hub'ları, Cosmos DB, SQL veritabanı, HBase, SignalR |C#, Java |
| [Hdınsight üzerinde Storm kullanarak Azure Event hubs'tan okumak için ölçeklenebilirlik değerlendirmeleri][d6c540e3] |İleti işleme, olay hub'ları, SQL veritabanı |C#, Java |
| [Hdınsight üzerinde Storm ve HBase kullanarak olayları ilişkilendirmenize](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Hdınsight üzerinde Storm ile Python kullanma](hdinsight-storm-develop-python-topology.md) |Bir Flux topolojisi ile Python bileşenleri |Python |
| [Hdınsight üzerinde Storm ile Kafka kullanın](hdinsight-apache-storm-with-kafka.md) | Apache Storm okuma ve yazma tooApache Kafka | Java |

### <a name="next-steps"></a>Sonraki Adımlar

* [HDInsight üzerinde Apache Storm kullanmaya başlama][2b8c3488]
* [Bilgi nasıl toodeploy ve Storm topolojileri Hdınsight üzerinde Storm ile yönetme][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Nasıl toocreate Hdınsight kümesi ve kullanım Storm hello Storm Panosu toodeploy örnek topolojileri öğrenin."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Bilgi nasıl toodeploy ve Visual Studio için hello web tabanlı Storm panosu ve Storm kullanıcı Arabirimi veya hello Hdınsight araçları kullanarak topolojiler yönetin."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Nasıl toocreate C# Storm topolojileri kullanarak Visual Studio için Hdınsight araçları hello öğrenin."
[5797064f]: hdinsight-storm-develop-java-topology.md "Bilgi nasıl toocreate Storm topolojilerini temel wordcount topoloji oluşturarak Maven kullanarak Java."
[94d15238]: hdinsight-storm-power-bi-topology.md "Gösteren nasıl toowrite veri tooPower bir C# topolojisi, BI'dan oluşturursunuz bir grafik ve Pano hello verileri."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "C# öğesinde uygulanan bir wordcount gerçekleştirir temel bir Storm topolojisini gösterir. Bu, aynı zamanda nasıl toocreate bir C# topolojisi içinde birden çok veri akışlarını gösterir."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Bilgi nasıl Hdınsight üzerinde Storm ile Azure Event hubs verilerini tooread ve yazma."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Azure Event Hubs, Hdınsight tooprocess algılayıcı verileri üzerinde Apache Storm toouse D3.js kullanarak görselleştirmek ve nasıl (isteğe bağlı olarak) tooHBase depolamak öğrenin."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Nasıl toouse Azure Event Hubs, Storm topolojisini tooread iletilerden veri başvurmak için Azure Cosmos DB'den belgeleri okuyun ve veri tooAzure depolama Kaydet öğrenin."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Hdınsight üzerinde Apache Storm kullanan Azure olay hub'larından okuma ve tooSQL Depolama veritabanı birkaç topolojileri toodemonstrate işleme."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Nasıl Azure Event Hubs, toplama & dönüştürme tooread verilerini veri Merhaba, ardından Hdınsight'ta tooHBase depolamak öğrenin."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Bu proje spout'lar, Cıvatalar ve Topolojileri toointeract Event Hubs, Cosmos DB ve SQL veritabanı gibi çeşitli Azure hizmetleriyle için şablonlar içerir."

