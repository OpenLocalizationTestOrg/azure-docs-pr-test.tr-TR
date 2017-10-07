---
title: "Azure Site RECOVERY'yi kullanarak aaaPrepare Azure kaynaklarını tooreplicate (System Center VMM ile) Hyper-V sanal makineleri tooAzure | Microsoft Docs"
description: "Hyper-V Vm'lerini (VMM ile) tooAzure çoğaltmaya Azure Site Recovery kullanmaya başlamadan önce Azure yerinde gerekenler açıklanmaktadır"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a>5. adım: Hyper-V çoğaltma (VMM ile) tooAzure için Azure kaynaklarını hazırlama

Doğruladıktan sonra [ağ gereksinimleri](vmm-to-azure-walkthrough-network.md), bu makale tooprepare Azure hello yönergeleri kullanın kaynakları şirket içi Hyper-V sanal makinelerini System Center Virtual Machine Manager (VMM) bulutlarında tooAzure içinde çoğaltabilirsiniz böylece kullanma Merhaba [Azure Site Recovery](site-recovery-overview.md) hizmet.

Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-an-azure-account"></a>Bir Azure hesabı ayarlama

- Alma bir [Microsoft Azure hesabı](http://azure.microsoft.com/).
- [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.
- Site Recovery, altında coğrafi kullanılabilirlik kısmına hello desteklenen bölgeleri kontrol [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
- Hakkında bilgi edinin [Site Recovery fiyatlandırma](site-recovery-faq.md#pricing)ve hello [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
- Azure hesabınızda hello doğru olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VM'ler. [Daha fazla bilgi edinin](../active-directory/role-based-access-built-in-roles.md) Azure rol tabanlı erişim denetimi hakkında.


## <a name="set-up-an-azure-network"></a>Azure ağı ayarlama

- Ayarlanmış bir [Azure ağ](../virtual-network/virtual-network-get-started-vnet-subnet.md). Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.
- Merhaba ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası
- Site Kurtarma'hello Azure portalı bölümünde ayarladığınız ağlar kullanabilir [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.
- Başlamadan önce bir ağ ayarlamanızı öneririz. Bunu yapmazsanız, toodo gerekir, Site Recovery dağıtımı sırasında.
- Hakkında bilgi edinin [sanal ağ fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Azure depolama hesabı ayarlama

- Site Recovery, şirket içi makineler tooAzure depolama çoğaltır. Yük devretme gerçekleştikten sonra azure VM'ler hello depolama biriminden oluşturulur.
- Standart/Premium'u ayarlama ayarlamak [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold veri çoğaltılan tooAzure.
- [Premium depolama](../storage/common/storage-premium-storage.md) sanal makineler için bir tutarlı bir şekilde yüksek g/ç performans ve düşük gecikme süresi toohost g/ç yoğun iş yükleri gerek genellikle kullanılır.
- Toouse istiyorsanız premium hesap toostore veri çoğaltılan, yakalama devam eden tooon içi verileri değiştiren bir standart depolama hesabı toostore çoğaltma günlükleri de gerekir.
- Merhaba kaynak modeline bağlı olarak toouse Azure vm'lerinde istediğiniz, hesap ayarlama [Resource Manager moduna](../storage/common/storage-create-storage-account.md), veya [Klasik modda](../storage/common/storage-create-storage-account.md).
- Başlamadan önce bir depolama hesabı ayarlamanız önerilir. Bunu yapmazsanız toodo gerekir, Site Recovery dağıtımı sırasında. Merhaba hesapları hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.
- Depolama hesapları kullanılan Site Recovery tarafından hello içindeki kaynak grupları arasında aynı taşıyamazsınız aboneliği ya da farklı Aboneliklerdeki.


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 6: VMM hazırlama](vmm-to-azure-walkthrough-vmm-hyper-v.md)
