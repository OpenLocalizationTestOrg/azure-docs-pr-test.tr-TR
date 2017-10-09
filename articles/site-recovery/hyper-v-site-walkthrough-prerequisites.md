---
title: "Azure Site Recovery kullanarak Hyper-V tooAzure çoğaltmayı (System Center VMM olmadan) aaaReview hello önkoşulları | Microsoft Docs"
description: "Çoğaltma, yük devretme ve şirket içi Hyper-V sanal makineleri tooAzure kurtarma Azure Site Recovery ile ayarlamak için hello önkoşulları açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>2. adım: Hyper-V (VMM olmadan) tooAzure çoğaltma hello önkoşullarını gözden geçirme

Merhaba Önkoşullar hello tabloda özetlenmiştir.


**Önkoşul** | **Ayrıntılar** 
--- | --- 
**Azure** | [Azure gereksinimleri](site-recovery-prereq.md#azure-requirements) hakkında bilgi edinin.
**Şirket içi sunucular** | [Daha fazla bilgi edinin](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) hello şirket içi Hyper-V konakları için gereksinimleri hakkında.
**Şirket içi Hyper-V VM'leri** | Tooreplicate çalışıyor istediğiniz sanal makineleri bir [işletim sistemi desteklenen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)ve uygun olması [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Azure URL'leri** | Hyper-V konakları toothese URL'leri erişim:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.<br/></br> Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.<br/></br> IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.



## <a name="next-steps"></a>Sonraki adımlar

- Tam dağıtımını yaptığınız, çok gidin[3. adım: kapasite planlama](hyper-v-site-walkthrough-capacity.md)
- Basit test dağıtımını yaptığınız, çok gidin[4. adım: ağ planlama](hyper-v-site-walkthrough-network.md).
