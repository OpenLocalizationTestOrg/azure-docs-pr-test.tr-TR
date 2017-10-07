---
title: "Hyper-V VM çoğaltma tooa Azure Site Recovery ile ikincil site için aaaMap ağları | Microsoft Docs"
description: "Hyper-V sanal makineleri tooa Azure Site Recovery ile ikincil VMM sitesi çoğaltırken toomap nasıl ağları açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>7. adım: Hyper-V VM çoğaltma tooa ikincil site için ağları Eşle


Ayarladıktan sonra [kaynak ve hedef ayarları](vmm-to-vmm-walkthrough-source-target.md) Hyper-V sanal makineleri (VM'ler) tooa ikincil System Center Virtual Machine Manager (VMM) site çoğaltmak için bu makale tooconfigure ağ eşlemesi için Hyper-V sanal kullanın Makine (VM) çoğaltma tooa ikincil site, kullanarak [Azure Site Recovery](site-recovery-overview.md).

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Başlamadan önce

- Hakkında bilgi edinin [ağ eşlemesi](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) başlamadan önce.
- Sanal makineler VMM sunucularında bağlı tooa VM ağı olduğundan emin olun.

## <a name="configure-network-mapping"></a>Ağ eşlemesini yapılandırma

1. İçinde **ağ eşlemesi** > **ağ eşlemeleri**, tıklatın **+ ağ eşlemesi**.
2. İçinde **ağ eşlemesi Ekle** sekmesinde hello kaynak seçin ve VMM sunucuyu hedefleyebilir. Merhaba VMM sunucular ile ilişkilendirilen hello VM ağları alınır.
3. İçinde **kaynak ağ**seçin toouse hello birincil VMM sunucusu ile ilişkili bir VM ağı hello listesinden istediğiniz hello ağ.
4. İçinde **hedef ağ**seçin hello ikincil VMM sunucusunda toouse istediğiniz hello ağ. Daha sonra, **Tamam**'a tıklayın.

    ![Ağ eşlemesi](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Ağ eşlemesi başladığında gerçekleşecekler şunlardır:

* Tüm mevcut çoğaltma toohello kaynak VM ağına karşılık gelen makineleri bağlı toohello hedef VM ağı olacaktır.
* Kaynak VM ağına bağlı toohello olan yeni sanal makinelere bağlı toohello hedef eşlenen ağ çoğaltma işleminden sonra olacaktır.
* Yeni bir ağ ile varolan bir eşlemesini değiştirirseniz, çoğaltma sanal makineleri hello yeni ayarlar kullanılarak bağlanır.
* Hello hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır. Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 8: bir çoğaltma ilkesi yapılandırma](vmm-to-vmm-walkthrough-replication.md).
