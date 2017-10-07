---
title: "Azure bölgeler arasında Azure Vm'leri aaaReplicate | Microsoft Docs"
description: "Merhaba adımlar, gerekli hello Azure portal'deki hello Azure Site Recovery hizmeti ile Azure bölgeler arasında tooreplicate Azure VM'ler özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Azure Site Recovery ile bölgeler arasında Azure Vm'lerini çoğaltma

>Bu makale bir Azure bölgesi tooAzure sanal makineleri farklı bir bölgede Azure sanal makinelerde (VM'ler) hello adımları gerekli tooreplicate genel bir bakış sağlar. 

>[!NOTE]
>
> Azure VM çoğaltma şu anda önizlemede değil.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="step-1-review-architecture"></a>1. adım: Gözden geçirme mimarisi

Dağıtıma başlamadan önce hello senaryo mimarisi ve toodeploy gereksinim hello bileşenleri gözden geçirin.

Çok Git[1. adım: gözden hello mimarisi](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>2. adım: Gözden geçirme önkoşulları

Sahip Merhaba, bir abonelik, sanal ağlar, depolama hesapları ve VM gereksinimleri çeşitli yerlerde Azure önkoşulları denetleyin.

Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>3. adım: ağ planlama

Giden bağlantı tooreplicate ve şirket içi bağlantılarından ayarlanır istediğiniz Azure vm'lerinde kurulduğundan emin olun.

Çok Git[4. adım: ağ planı](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>4. adım: bir kasa oluşturma 

Kurtarma Hizmetleri kasası tooorchestrate yukarı tooset gerekir ve çoğaltmayı yönetmek ve hello kaynak bölge belirtin.

Çok Git[4. adım: bir kasa oluşturun](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>5. adım: Çoğaltma etkinleştirme


tooenable çoğaltma hedef konumu ayarları yapılandırmak, bir çoğaltma ilkesini ayarlayın ve hello Azure tooreplicate istediğiniz sanal makineleri seçin. Etkinleştirdikten sonra ilk çoğaltma işlemi hello VM oluşur.

Çok Git[5. adım: çoğaltmasını etkinleştir](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>6. adım: yük devretme testi çalıştırma

İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırabilirsiniz.

Çok Git[6. adım: yük devretme testi çalıştırma](azure-to-azure-walkthrough-test-failover.md)


