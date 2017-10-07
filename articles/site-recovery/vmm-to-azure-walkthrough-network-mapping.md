---
title: "vmm'de Hyper-V Vm'lerini çoğaltma için aaaConfigure ağ eşlemesi bulut Azure Site Recovery ile tooAzure | Microsoft Docs"
description: "Vmm'de Hyper-V sanal makineleri çoğaltırken tooconfigure ağ eşlemesi tooAzure Azure Site Recovery ile nasıl Bulutlar açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>9. adım: Hyper-V çoğaltma (VMM ile) tooAzure için ağ eşlemesini yapılandırma

Merhaba ayarladıktan sonra [kaynak ve hedef çoğaltma ayarları](vmm-to-azure-walkthrough-source-target.md), bu makale tooconfigure ağ eşlemesi toomap şirket içi VMM VM ağları ve Azure ağları arasında kullanın.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Başlamadan önce

- Hakkında bilgi edinin [ağ eşlemesi](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- [VMM ağ eşlemesi için hazırlanma](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- Sanal makineler hello VMM sunucusunda bağlı tooa VM ağı olduğunu ve en az bir Azure sanal ağı oluşturduğunuzu doğrulayın. Birden fazla VM ağı eşlenen tooa tek Azure ağ olabilir.

## <a name="configure-mapping"></a>Eşlemeyi yapılandırın

Eşleme işlemini şu şekilde yapılandırın:

1. İçinde **Site Recovery altyapısı** > **ağ eşlemeleri** > **ağ eşlemesi**, hello tıklatın **+ ağ eşlemesi**  simgesi.

    ![Ağ eşlemesi](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. İçinde **ağ eşlemesi Ekle**seçin hello kaynak VMM sunucusunu ve **Azure** hello hedefi olarak.
3. Yük devretme sonrasında Hello abonelik ve hello dağıtım modeli doğrulayın.
4. İçinde **kaynak ağ**seçin hello kaynak şirket içi VM ağını hello VMM sunucusuyla ilişkili hello listeden toomap istiyor.
5. İçinde **hedef ağ**, hello hangi çoğaltma Azure VM'ler konumlandırılacağı oluşturuldukları zaman Azure ağı seçin. Daha sonra, **Tamam**'a tıklayın.

    ![Ağ eşlemesi](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

Ağ eşlemesi başladığında gerçekleşecekler şunlardır:

* Eşleme başladığında hello kaynak VM ağındaki VM'ler bağlı toohello hedef ağ tabanlıdır. Yeni sanal makineleri bağlı toohello kaynak VM ağına bağlı Çoğaltma gerçekleştiğinde eşlenen Azure ağ toohello.
* Varolan bir ağ eşlemesini değiştirirseniz, çoğaltma sanal makineleri hello yeni ayarları kullanarak bağlanır.
* Merhaba hedef ağ birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında toothat hedef alt bağlanır.
* Eşleşen ada sahip bir hedef alt ağ varsa, hello sanal makine toohello hello ağdaki ilk alt ağa bağlanır.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 10: bir çoğaltma ilkesi oluşturun](vmm-to-azure-walkthrough-replication.md)
