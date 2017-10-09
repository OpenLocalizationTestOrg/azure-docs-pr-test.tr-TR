---
title: "aaaAn giriş tooApache hdınsight'ta - Azure Kafka | Microsoft Docs"
description: "Hdınsight üzerinde Apache Kafka hakkında bilgi edinin: toofind örnekler ve alma bilgilerini başlatıldığı nedir ve ne yaptığını."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>HDInsight üzerinde Apache Kafka’ya giriş (önizleme)

[Apache Kafka](https://kafka.apache.org) kullanılan toobuild gerçek zamanlı olabilir bir açık kaynak dağıtılmış akış platform veri ardışık düzen ve uygulamaları akış. Kafka, burada yayımlayın ve toonamed veri akışları abone işlevselliği benzer tooa ileti sırası, ileti Aracısı de sağlar. Hdınsight üzerinde Kafka hello Microsoft Azure bulutta yönetilen, ölçeklendirilebilir ve yüksek oranda kullanılabilir bir hizmet sağlar.

## <a name="why-use-kafka-on-hdinsight"></a>HDInsight üzerinde Kafka neden kullanılmalıdır?

Kafka hello aşağıdaki özellikleri sağlar:

* Mesajlaşma düzeni yayımlama-abonelik: Kafka kayıtları tooa Kafka konu yayımlamak için bir üretici API sağlar. Merhaba tüketici API tooa konu abone olduğunda kullanılır.

* Akış işleme: Kafka genellikle gerçek zamanlı akış işleme için Apache Storm veya Spark ile birlikte kullanılır. Kafka 0.10.0.0 (Hdınsight sürüm 3.5) çözümleri gerektirmeden Storm veya Spark akış toobuild sağlayan bir akış API sunmuştur.

* Yatay Ölçek: Kafka hello Hdınsight kümesinde hello düğümleri arasında akışları bölümler. Tüketici işlemleri ayrı ayrı bölümleri tooprovide yük kayıtları kullanırken dengelemesi ile ilişkilendirilebilir.

* Sıralı teslim: her bölüm içinde kayıtları hello akış bunlar alınan hello sırayla depolanır. Bölüm başına bir tüketici işlemi ile ilişkilendirerek, kayıtların sırayla işlenmesini garanti edebilirsiniz.

* Hataya dayanıklı: Bölümleri arasında düğümleri tooprovide hata toleransı çoğaltılabilir.

* Azure yönetilen diskler ile tümleştirme: yönetilen diskleri sağlayan daha yüksek ölçek ve verimlilik hello Hdınsight kümesi hello sanal makineler tarafından kullanılan hello diskler.

    Yönetilen diskleri hdınsight'ta Kafka için varsayılan olarak etkindir ve düğüm başına kullanılan diskler hello sayısı Hdınsight oluşturma sırasında yapılandırılabilir. Yönetilen diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Diskler](../virtual-machines/windows/managed-disks-overview.md).

    Yönetilen disklerin HDInsight üzerinde Kafka ile yapılandırılması hakkında bilgi edinmek için bkz. [HDInsight üzerinde Kafka'nın ölçeklenebilirliğini artırma](hdinsight-apache-kafka-scalability.md).

## <a name="use-cases"></a>Uygulama alanları

* **İleti**: hello desteklediğinden yayımlama-abone ileti deseni, Kafka genellikle bir ileti aracı olarak kullanılır.

* **İzleme etkinliği**: bu yana Kafka kayıtları sıralı günlüğe kaydedilmesini sağlar, kullanılan tootrack olması ve etkinlikleri yeniden oluşturun. Örneğin, bir web sitesindeki veya uygulamadaki kullanıcı işlemleri.

* **Toplama**: akış işleme kullanan, farklı akışları toocombine bilgileri toplamak ve işletimsel veri hello bilgileri merkezileştirme.

* **Dönüştürme**: Akış işlemeyi kullanarak, birden fazla girdi konu başlığındaki verileri bir veya daha fazla çıktı konu başlığında birleştirerek verileri zenginleştirebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

Kullanım hello aşağıdaki bağlantılar toolearn nasıl toouse Hdınsight üzerinde Apache Kafka:

* [HDInsight'ta Kafka kullanmaya başlama](hdinsight-apache-kafka-get-started.md)

* [Hdınsight üzerinde MirrorMaker toocreate Kafka bir kopyasını kullan](hdinsight-apache-kafka-mirroring.md)

* [Apache Storm’u HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-storm-with-kafka.md)

* [Apache Spark’ı HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-spark-with-kafka.md)

* [Bir Azure sanal ağı tooKafka Bağlan](hdinsight-apache-kafka-connect-vpn-gateway.md)
