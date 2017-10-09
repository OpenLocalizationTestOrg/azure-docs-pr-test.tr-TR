---
title: "aaaUpgrade Hdınsight küme tooa daha yeni sürümü-Azure | Microsoft Docs"
description: "Nasıl tooUpgrade Hdınsight küme tooa daha yeni sürüm bilgi edinin."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>Hdınsight küme tooa daha yeni sürümüne yükseltin
tootake avantajlarından Merhaba son Hdınsight özellikleri, Hdınsight kümeleri yükseltilmiş toolatest sürüm olmasını öneririz. Merhaba yönergeleri tooupgrade aşağıda Hdınsight küme sürümleri izleyin.

> [!NOTE]
> Hdınsight kümesi sürüm 3.2 ve 3.3 tarihten dolmak üzere. Hdınsight'ın desteklenen sürümünü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md#supported-hdinsight-versions).
>
>

## <a name="upgrade-tasks"></a>Yükseltme görevleri
Merhaba iş akışı tooupgrade Hdınsight kümesi aşağıdaki gibidir.

![Yükseltme iş akışı diyagramı](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. Bu belgenin her bölüm Hdınsight kümenize yükseltirken gerekli olabilecek toounderstand değişiklikleri okuyun.
2. Bir küme bir test/kalite güvence ortamı oluşturun. Küme oluşturma ile ilgili daha fazla bilgi için bkz: [nasıl toocreate Linux tabanlı Hdınsight kümeleri öğrenin](hdinsight-hadoop-provision-linux-clusters.md)
3. İşleri, veri kaynakları ve havuzlarını toohello yeni ortam varolan kopyalayın. Bkz: [veri Kopyala tooTest ortam](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) daha fazla ayrıntı için.
4. Toomake işleriniz hello yeni kümede beklendiği gibi çalıştığından emin sınama doğrulaması gerçekleştirir.


Her şeyin beklendiği gibi çalıştığını doğruladıktan sonra hello geçiş için kapalı kalma süresi zamanlayın. Bu kesinti sırasında aşağıdaki işlemleri hello:

1.  Merhaba küme düğümlerinde yerel olarak depolanan tüm geçici verileri yedekleyin. Örneğin, doğrudan bir baş düğüm üzerinde depolanan verileri varsa.
2.  Merhaba var olan küme silin.
3.  Bir küme oluşturmak hello kullanılan önceki küme hello aynı varsayılan veri deposu hello VNET en son (veya desteklenen) olan bir alt ağ HDI sürümü kullanarak aynı. Bu, var olan üretim verileriyle çalışma hello yeni küme toocontinue sağlar.
4.  Yedeklediğiniz herhangi bir geçici veri içeri aktarın.
5.  Başlangıç işleri/hello yeni küme kullanarak işlemeye devam et.

## <a name="next-steps"></a>Sonraki Adımlar
* [Nasıl toocreate Linux tabanlı Hdınsight kümeleri öğrenin](hdinsight-hadoop-provision-linux-clusters.md)
* [SSH kullanarak tooHDInsight Bağlan](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Ambari kullanarak Linux tabanlı bir kümeyi yönetmek](hdinsight-hadoop-manage-ambari.md)

