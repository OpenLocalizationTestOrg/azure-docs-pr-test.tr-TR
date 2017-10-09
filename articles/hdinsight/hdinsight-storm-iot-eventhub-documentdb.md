---
title: "Hdınsight üzerinde Apache Storm ile aaaProcess araç algılayıcı verilerini | Microsoft Docs"
description: "Bilgi nasıl tooprocess araç algılayıcı verileri olay hub'ın Hdınsight üzerinde Apache Storm kullanma. Model verileri Azure Cosmos DB'den ekleyin ve çıktı toostorage depolar."
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
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Hdınsight üzerinde Apache Storm kullanan Azure Event Hubs araç algılayıcı verilerini işlemek

Bilgi nasıl Hdınsight üzerinde Apache Storm kullanan Azure Event Hubs tooprocess araç algılayıcı verilerini. Bu örnek, Azure Event Hubs'tan gelen algılayıcı verilerini okur, Azure Cosmos DB içinde depolanan verileri başvurarak hello veri aşağıdakilere zenginleştirir. Merhaba veri hello Hadoop dosya sistemi (HDFS) kullanarak Azure depolama alanına depolanır.

![Hdınsight ve hello nesnelerin interneti (IOT) mimarisi diyagramı](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Genel Bakış

Algılayıcılar toovehicles ekleme geçmiş verileri eğilimler temelinde toopredict donanım sorunları sağlar. Ayrıca, toomake geliştirmeleri kullanım deseni analize dayalı toofuture sürümleri sağlar. Mümkün tooquickly olması ve MapReduce işleme oluşabilmesi için öncelikle hello verileri Hadoop tüm araçlar verimli bir şekilde yükleyin. Ayrıca, gerçek zamanlı olarak kritik hata yolları (altyapısı sıcaklık, Frenler, vb.) toodo analize isteyebilir.

Azure Event Hubs toohandle hello yoğun algılayıcılar tarafından üretilen verilerin hacmi yerleşik olarak bulunur. Apache Storm kullanılan tooload ve işlem hello verileri HDFS depolamadan önce olabilir.

## <a name="solution"></a>Çözüm

Telemetri verileri altyapısı sıcaklık, ortam sıcaklık ve araç hızı algılayıcılar tarafından kaydedilir. Veri tooEvent hub hello otomobilin araç kimlik numarası (Toplamıdır) ve zaman damgası ile birlikte gönderilir. Buradan, Apache Storm Hdınsight kümesi üzerinde çalışan Storm topolojisini hello verileri okur, işler ve HDFS depolar.

İşleme sırasında kullanılan tooretrieve modelle Cosmos DB'den hello Toplamıdır var. Bu verilerin depolandığı önce toohello veri akışı eklenir.

Merhaba Storm topolojisini kullanılan hello bileşenleri şunlardır:

* **EventHubSpout** -Azure Event Hubs'tan gelen verileri okur
* **TypeConversionBolt** -hello algılayıcı verilerini aşağıdaki hello içeren bir tanımlama grubu Event hubs'dan JSON dizeye dönüştürür:
    * Altyapısı sıcaklık
    * Ortam sıcaklık
    * Hız
    * TOPLAMIDIR
    * zaman damgası
* **DataReferencBolt** -Cosmos hello Toplamıdır kullanarak DB'den hello araç modelini arar
* **WasbStoreBolt** -depoları hello veri tooHDFS (Azure depolama)

Görüntü aşağıdaki hello Bu çözüm diyagramı şöyledir:

![Storm topolojisi](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Uygulama

Tam, otomatik çözüm bu senaryo için hello bir parçası olarak [Hdınsight Storm örnekler](https://github.com/hdinsight/hdinsight-storm-examples) github'daki. toouse Bu örnekte, hello adımları hello içinde [IoTExample Benioku. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Sonraki Adımlar

Daha fazla örnek Storm Topolojileri için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).

