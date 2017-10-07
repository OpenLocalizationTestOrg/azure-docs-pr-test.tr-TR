---
title: "aaaReplicate fiziksel şirket içi sunucuları tooAzure Azure Site Recovery ile | Microsoft Docs"
description: "Şirket içi Windows/Linux fiziksel sunucuları tooAzure hello Azure Site Recovery hizmeti ile çalışan iş yükleri çoğaltmak için hello adımlara genel bir bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Site Recovery ile fiziksel sunucuları tooAzure Çoğalt

Bu makalede hello kullanarak hello adımları gerekli tooreplicate şirket içi Windows/Linux fiziksel sunucuları tooAzure, genel bir bakış sağlar [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.


## <a name="step-1-review-architecture-and-prerequisites"></a>1. adım: mimarisi ve önkoşulları gözden geçirin

Dağıtıma başlamadan önce hello senaryo mimarisinin gözden geçirin ve hello dağıtım tooset gerek duyduğunuz tüm hello bileşenleri anladığınızdan emin olun.

Çok Git[1. adım: gözden hello mimarisi](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>2. adım: Gözden geçirme önkoşulları

Merhaba Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:

- **Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.
- **Şirket içi Site Recovery bileşenlerini**: şirket içi Site Recovery bileşenlerini çalıştıran bir makineye gerekir.
- **Makineler çoğaltılan**: tooreplicate istediğiniz sunucuları şirket içi ve Azure gereksinimleri ile toocomply gerekir.

Çok Git[2. adım: gözden Önkoşullar ve sınırlamalar](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>3. adım: Planı kapasite

Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları çıkışı toofigure gerekir. Tootest hello ortamını ayarlama hızlı yaptığınız varsa, bu adımı atlayabilirsiniz.

Çok Git[3. adım: kapasite planlama](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>4. adım: ağ planlama

Yük devretme gerçekleştikten sonra Azure Vm'lerinin bağlı toonetworks olduğunu ve sahip oldukları hello doğru IP adreslerine tooensure planlama bazı ağ toodo gerekir.

Çok Git[4. adım: ağ planı](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>5. adım: Azure kaynaklarını hazırlama

Başlamadan önce Azure ağları ve depolama ayarlayın. 

Çok Git[5. adım: Azure hazırlama](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>6. adım: Bir kasa ayarlama

Kurtarma Hizmetleri kasası tooorchestrate ayarlamak ve çoğaltmayı yönetme. Merhaba kasasını ayarladığınızda, istediğinizi belirtin tooreplicate, ve tooreplicate istediğiniz şekilde.

Çok Git[adım 6: bir kasasını oluşturup](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>7. adım: kaynak ve hedef ayarlarını yapılandırma

Merhaba kaynağı için ayarları yapılandırın ve hedef (Azure). Kaynak ayarları birleşik Kurulum tooinstall hello şirket içi Site Recovery bileşenlerini çalıştıran içerir.

Çok Git[adım 7: hello kaynak ve hedef ayarlama](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>8. adım: Bir çoğaltma ilkesi ayarlama

İlke toospecify nasıl fiziksel ayarladığınız sunucuları çoğaltır.

Çok Git[adım 8: bir çoğaltma ilkesini ayarlayın](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>9. adım: hello Mobility hizmetini yükleme

Merhaba mobilite hizmetinin yüklenmesi tooreplicate istediğiniz her sunucuda. Merhaba hizmetiyle iterek ister çekerek yükleme yukarı birkaç yolu tooset vardır.

Çok Git[adım 9: hello Mobility hizmetini yükleme](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>10. adım: Çoğaltma etkinleştirme

Merhaba Mobility hizmeti bir sunucuda çalıştırdıktan sonra çoğaltmayı etkinleştirebilirsiniz. Etkinleştirdikten sonra ilk çoğaltma işlemi hello VM oluşur.

Çok Git[adım 10: çoğaltmasını etkinleştir](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>11. adım: yük devretme testi çalıştırma

İlk çoğaltma sonlandırıldıktan sonra değişim çoğaltması çalıştığından, bir test yük devretme toomake her şeyin beklendiği gibi çalıştığından emin çalıştırabilirsiniz.

Çok Git[11. adım: yük devretme testi çalıştırma](physical-walkthrough-test-failover.md)

