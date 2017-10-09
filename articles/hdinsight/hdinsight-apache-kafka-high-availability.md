---
title: "Apache Kafka - Azure Hdınsight ile aaaHigh kullanılabilirliğini | Microsoft Docs"
description: "Bilgi nasıl tooensure yüksek kullanılabilirlik ile Azure hdınsight'ta Apache Kafka. Nasıl toorebalance bölüm kopyalarını Kafka böylece Hdınsight içeren Azure bölgesi hello farklı hata etki alanlarını üzerinde olduğu hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>HDInsight’ta Apache Kafka (önizleme) ile verilerinizin yüksek kullanılabilirliği

Temel alınan donanım Kafka konuları tootake avantajlarından tooconfigure çoğaltmalarını yapılandırma nasıl raf öğrenin. Bu yapılandırma, Hdınsight üzerinde Apache Kafka depolanan verileri hello kullanılabilirliğini sağlar.

## <a name="fault-and-update-domains-with-kafka"></a>Kafka ile hata ve güncelleme etki alanları

Hata etki alanı, bir Azure veri merkezinde temel donanımlardan oluşan mantıksal bir gruplandırmadır. Her hata etki alanı ortak bir güç kaynağı ve ağ anahtarına sahiptir. Bu hata etki alanlarında Hello sanal makineler ve Hdınsight kümesi içinde hello düğümleri uygulamak yönetilen diskleri dağıtılır. Bu mimari, fiziksel donanım hatalarının olası etkisini hello sınırlar.

Her Azure bölgesinde belirli sayıda hata etki alanı bulunur. Merhaba etki alanları ve içerdikleri hata etki alanı hello sayısı listesi için bkz [kullanılabilirlik kümeleri](../virtual-machines/linux/regions-and-availability.md#availability-sets) belgeleri.

> [!IMPORTANT]
> Kafka, hata etki alanları ile uyumlu değildir. Kafka bir konu oluşturduğunuzda, tüm çoğaltmalarını hello depolayabilir aynı hata etki alanı. toosolve hello sağladığımız Bu sorun [Kafka bölüm yeniden dengeleyin aracını](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-toorebalance-partition-replicas"></a>Ne zaman toorebalance bölüm çoğaltmaları

Kafka verilerinizin tooensure hello yüksek kullanılabilirlik, size hello çoğaltmalarını Konunuzu kez hello adresindeki için yeniden dengelemeniz gerekir:

* Yeni bir konu veya bölüm oluşturulduğunda

* Bir kümenin ölçeğini artırdığınızda

## <a name="replication-factor"></a>Çoğaltma faktörü

> [!IMPORTANT]
> Üç hata etki alanı içeren ve çoğaltma faktörü 3 olan bir Azure bölgesi kullanmanız önerilir.

Yalnızca iki hata etki alanları içeren bir bölge kullanmanız gerekiyorsa, bir çoğaltma faktörü 4 toospread hello çoğaltmalarının hello iki hata etki alanları arasında eşit olarak kullanın.

Hello konuları ve ayarı hello çoğaltma faktörü oluşturma örneği için bkz: [hdınsight'ta Kafka başlayarak](hdinsight-apache-kafka-get-started.md) belge.

## <a name="how-toorebalance-partition-replicas"></a>Nasıl toorebalance bölüm çoğaltmaları

Kullanım hello [Kafka bölüm yeniden dengeleyin aracını](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance Seçili konular. Bu aracı gerekir olması çalıştırdım bir SSH oturumu toohello baş düğümünden Kafka kümenizin.

SSH kullanarak tooHDInsight bağlama hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.

## <a name="next-steps"></a>Sonraki adımlar

* [HDInsight’ta Kafka ölçeklenebilirliği](hdinsight-apache-kafka-scalability.md)
* [HDInsight'ta Kafka ile yansıtma](hdinsight-apache-kafka-mirroring.md)