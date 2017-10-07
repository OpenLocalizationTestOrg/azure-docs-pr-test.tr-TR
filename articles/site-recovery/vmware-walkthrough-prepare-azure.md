---
title: "aaaPrepare Azure kaynaklarını tooreplicate şirket içi VMware sanal makinelerini tooAzure Azure Site RECOVERY'yi kullanarak | Microsoft Docs"
description: "Azure Site RECOVERY'yi kullanarak şirket içi VMware sanal makinelerini tooAzure çoğaltma başlamadan önce Azure yerinde gerekenler açıklanmaktadır"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a>5. adım: VMWare çoğaltma tooAzure için Azure kaynaklarını hazırlama


Bu makale tooprepare Azure Hello yönergeleri kullanın kaynakları böylece şirket içi makineler tooAzure hello kullanarak çoğaltabilirsiniz [Azure Site Recovery](site-recovery-overview.md) hizmet.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Başlamadan önce

Emin olun hello okuma [önkoşulları](vmware-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Bir Azure hesabı ayarlama

- Alma bir [Microsoft Azure hesabı](http://azure.microsoft.com/).
- [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.
- Site Recovery, altında coğrafi kullanılabilirlik kısmına hello desteklenen bölgeleri kontrol [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
- Hakkında bilgi edinin [Site Recovery fiyatlandırma](site-recovery-faq.md#pricing)ve hello [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Azure ağı ayarlama

- Azure ağı ayarlama ayarlayın. Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.
- Site Kurtarma'hello Azure portalı bölümünde ayarladığınız ağlar kullanabilir [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.
- Merhaba ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası
- Hakkında bilgi edinin [sanal ağ fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-network/).
- Daha fazla bilgi edinmek [Azure VM bağlantı](site-recovery-network-design.md) yük devretme sonrasında.


## <a name="set-up-an-azure-storage-account"></a>Azure depolama hesabı ayarlama

- Site Recovery, şirket içi makineler tooAzure depolama çoğaltır. Yük devretme gerçekleştikten sonra azure VM'ler hello depolama biriminden oluşturulur.
- Ayarlanmış bir [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) çoğaltılan veriler için.
- Site Kurtarma'hello Azure portal Kaynak Yöneticisi'nde veya Klasik modda ayarlanmış depolama hesaplarını kullanabilirsiniz.
- Merhaba depolama hesabı standart olabilir veya [premium](../storage/common/storage-premium-storage.md).
- Premium hesabınızı ayarlarsanız, ek bir standart hesap için günlük verileri gerekir.


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 6: hazırlama VMware kaynakları](vmware-walkthrough-prepare-vmware.md)
