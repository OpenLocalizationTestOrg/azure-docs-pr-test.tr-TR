---
title: "Hdınsight üzerinde Apache Storm ile araç algılayıcı verilerini işlemek | Microsoft Docs"
description: "Event Hubs Hdınsight üzerinde Apache Storm kullanan araç algılayıcı verilerini işlemek öğrenin. Model verileri Azure Cosmos DB'den ekleyin ve depolama birimine çıkış depolamak."
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8e8ebc724e1c70e8fcd56312adef5da2342373ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Hdınsight üzerinde Apache Storm kullanan Azure Event Hubs araç algılayıcı verilerini işlemek

Hdınsight üzerinde Apache Storm kullanan Azure Event Hubs araç algılayıcı verilerini işlemek öğrenin. Bu örnek, Azure Event Hubs'tan gelen algılayıcı verilerini okur, verileri Azure Cosmos DB içinde depolanan verileri başvurarak aşağıdakilere zenginleştirir. Verileri Hadoop dosya sistemi (HDFS) kullanarak Azure depolama alanına depolanır.

![Hdınsight ve nesnelerin interneti (IOT) mimarisi diyagramı](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Genel Bakış

Algılayıcılar için Araçlar ekleme, geçmiş verileri eğilimler temelinde donanım sorunları tahmin etmek sağlar. Ayrıca, kullanım deseni analize dayalı gelecek sürümlerinde geliştirmeleri yapmanızı sağlar. MapReduce işleme oluşabilmesi için öncelikle hızlı ve verimli şekilde verileri tüm araçlar Hadoop yüklemek. olması gerekir. Ayrıca, gerçek zamanlı Kritik hata yolları (altyapısı sıcaklık, Frenler, vb.) için analizi yapmak isteyebilirsiniz.

Azure Event Hubs büyük algılayıcılar tarafından oluşturulan veri hacmi işlemek için yerleşik olarak bulunur. Apache Storm, yüklemek ve HDFS depolamadan önce verileri işlemek için kullanılabilir.

## <a name="solution"></a>Çözüm

Telemetri verileri altyapısı sıcaklık, ortam sıcaklık ve araç hızı algılayıcılar tarafından kaydedilir. Verileri Event hubs'a otomobilin araç kimlik numarası (Toplamıdır) ve zaman damgası ile birlikte gönderilir. Buradan Apache Storm Hdınsight kümesi üzerinde çalışan Storm topolojisini veri okur, işler ve HDFS depolar.

İşleme sırasında Toplamıdır modelle Cosmos DB'den almak için kullanılır. Depolandığı önce bu verileri veri akışına eklenir.

Storm topolojisinde kullanılan bileşenleri şunlardır:

* **EventHubSpout** -Azure Event Hubs'tan gelen verileri okur
* **TypeConversionBolt** -JSON dizesi olay hub'larından aşağıdaki algılayıcı verilerini içeren bir tanımlama grubu dönüştürür:
    * Altyapısı sıcaklık
    * Ortam sıcaklık
    * Hız
    * TOPLAMIDIR
    * zaman damgası
* **DataReferencBolt** -Cosmos Toplamıdır kullanarak DB'den araç modelini arar
* **WasbStoreBolt** -HDFS (Azure Storage) veri depolar

Aşağıdaki resimde bir diyagram bu çözümün şöyledir:

![Storm topolojisi](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Uygulama

Tam, otomatik çözüm olarak bu senaryoda kullanılabilir parçası [Hdınsight Storm örnekler](https://github.com/hdinsight/hdinsight-storm-examples) github'daki. Bu örneği kullanmak için adımları [IoTExample Benioku. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Sonraki Adımlar

Daha fazla örnek Storm Topolojileri için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).

