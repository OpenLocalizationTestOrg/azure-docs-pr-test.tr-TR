---
title: "Linux tabanlı Hdınsight kümeleri - Azure aaaConfigure OS düzeltme eki uygulama zamanlama | Microsoft Docs"
description: "Nasıl tooconfigure OS düzeltme eki uygulama zamanlamasını Linux tabanlı Hdınsight kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>İşletim sistemi Hdınsight için düzeltme eki uygulama 
Yönetilen bir Hadoop hizmet olarak Hdınsight hello işletim sistemi temel VM'ler Hdınsight kümeleri tarafından kullanılan Merhaba, düzeltme eki uygulama mvc'deki. 1 Ağustos 2016 itibariyle biz hello konuk işletim sistemi düzeltme eki uygulama ilkesi Linux tabanlı Hdınsight kümeleri (sürüm 3.4 veya büyük) için değiştirilmiştir. Merhaba hello yeni ilke hedefidir toosignificantly yeniden başlatmalar hello sayısını azaltın son toopatching. Merhaba yeni ilke toopatch sanal makinelerde (VM'ler) Linux kümeleri her Pazartesi ya da verilmiş bir küme düğümleri arasında 00: 00 UTC aşamalı bir şekilde başlayarak Perşembe devam eder. Ancak, belirli bir VM yalnızca en fazla 30 tooguest OS düzeltme eki uygulama son günde bir kez yeniden başlatılır. Ayrıca, yeni oluşturulan bir küme için hello ilk yeniden başlatma hello küme oluşturma tarihten itibaren 30 gün daha erken yapılmaz. Merhaba VM'ler yeniden sonra düzeltme eklerini etkili olacaktır.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>Nasıl tooconfigure hello Linux tabanlı Hdınsight kümeleri için işletim sistemi düzeltme eki uygulama zamanlama
Hdınsight kümesi Hello sanal makineniz önemli güvenlik düzeltme ekleri yüklenmemiş böylece bazen yeniden toobe olması gerekir. 1 Ağustos 2016 itibariyle yeni Linux tabanlı Hdınsight kümeleri (sürüm 3.4 veya daha büyük) yeniden zamanlama uyarınca hello kullanarak:

1. Merhaba kümesindeki bir sanal makine yalnızca düzeltme ekleri için en fazla bir kez bir 30 günlük süre içinde yeniden başlatabilirsiniz.
2. 00: 00 UTC başlayarak Hello yeniden başlatma gerçekleşir.
3. Merhaba küme hello yeniden başlatma işlemi sırasında hala kullanılabilir olacak şekilde hello kümedeki sanal makineler arasında hello yeniden başlatma işlemi aşamalı.
4. Yeni oluşturulan bir küme için Hello ilk yeniden başlatma hello küme oluşturma tarihinden sonra 30 günden daha erken yapılmaz.

Bu makalede açıklanan hello betik eylemi kullanarak, hello OS düzeltme eki uygulama zamanlamasını aşağıdaki gibi değiştirebilirsiniz:
1. Etkinleştirmek veya devre dışı otomatik yeniden başlatma
2. Set hello sıklığı (gün yeniden başlatmalar arasında) yeniden başlatır
3. Merhaba haftanın günü için yeniden başlatma oluştuğunda hello ayarlayın

> [!NOTE]
> Bu betik eylemi yalnızca 1 Ağustos 2016'dan sonra oluşturulan Linux tabanlı Hdınsight kümeleri ile çalışır. Yalnızca sanal makineleri yeniden, düzeltme ekleri etkili olur. 
>

## <a name="how-toouse-hello-script"></a>Nasıl toouse hello komut dosyası 

Ne zaman bu komut dosyasını kullanarak aşağıdaki bilgilerle hello gerektirir:
1. Merhaba komut dosyası konumu: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  Hdınsight bu URI toofind kullanır ve hello kümedeki tüm hello sanal makinelerde hello komut dosyasını çalıştırın.
  
2. Merhaba hello betik uygulandığı Küme düğüm türleri: headnode, workernode, zookeeper. Bu komut dosyası uygulanan tooall düğüm türleri hello kümedeki olması gerekir. Uygulanan tooa düğüm türü sonra hello sanal değilse bu düğüm türü için makineler toouse hello önceki düzeltme eki uygulama zamanlama devam eder.


3.  Parametre: Bu komut dosyasını üç sayısal parametreleri kabul eder:

    | Parametre | Tanım |
    | --- | --- |
    | Otomatik yeniden başlatmalar etkinleştir/devre dışı bırak |0 veya 1. Otomatik yeniden başlatmalar 1 olanak sağlarken otomatik yeniden başlatmalar 0 değerini devre dışı bırakır. |
    | Sıklık |7 too90 (dahil). Merhaba sanal makineleri yeniden başlatılması düzeltme ekleri için yeniden başlatmadan önce gün toowait Hello sayısı. |
    | Haftanın günü |1 too7 (dahil). 1 değeri hello yeniden başlatma, Pazartesi günü gerçekleşmelidir, 7 parametrelerini kullanarak bir Sunday.For örnek belirtir 1 60 2 sonuçları otomatik olarak yeniden başlatılır 60 günde (en çok) Salı günü. |
    | Kalıcılığı |Bir komut dosyası eylemi tooan var olan küme uygularken hello betik kalıcı olarak işaretleyebilirsiniz. Yeni workernodes toohello küme işlemleri ölçeklendirme aracılığıyla eklenen kalıcı betikleri uygulanır. |

> [!NOTE]
> Bu komut dosyası tooan var olan küme uygularken kalıcı olarak işaretlemeniz gerekir. Aksi takdirde, işlemleri ölçeklendirme aracılığıyla oluşturulan tüm yeni düğümler hello varsayılan zamanlama düzeltme eki uygulama kullanır.
Merhaba küme oluşturma işleminin bir parçası olarak hello betik uygularsanız, otomatik olarak kalıcıdır.
>

## <a name="next-steps"></a>Sonraki adımlar

Merhaba betik eylemi kullanarak hakkında belirli adımlar için bkz hello bölümlerde aşağıdaki hello [özelleştirme Linuz tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md):

* [Küme oluşturma sırasında bir betik eylemi kullanın](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [Küme çalışan bir komut dosyası eylemi tooa Uygula](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
