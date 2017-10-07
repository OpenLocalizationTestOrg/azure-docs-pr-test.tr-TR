---
title: "Hedef (VMware tooAzure) hazırlama | Microsoft Docs"
description: "Bu makalede nasıl tooprepare, Azure ortamı toostart VMware sanal makineleri tooAzure çoğaltılıyor."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Hedef (VMware tooAzure) hazırlama
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [Fiziksel tooAzure](./site-recovery-prepare-target-physical-to-azure.md)

Bu makalede nasıl tooprepare, Azure ortamı toostart VMware sanal makineleri tooAzure çoğaltılıyor.

## <a name="prerequisites"></a>Ön koşullar

Merhaba makale hello aşağıdakileri varsayar:
- VMware sanal makineleri kurtarma Hizmetleri kasası tooprotect oluşturdunuz. Bir kurtarma Hizmetleri kasası hello oluşturabilirsiniz [Azure portal](http://portal.azure.com "Azure portal").
- Sahip olduğunuz [, şirket içi ortamınızın Kurulumu](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware sanal makineleri tooAzure.

## <a name="prepare-target"></a>Hedef hazırlama

Merhaba tamamladıktan sonra **adım 1:Select koruma hedefi** ve **2. adım: kaynak hazırlama**, çok alınır**adım 3: hedef**

![Hedef hazırlama](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. **Abonelik:** , sanal makinelerinizin hello açılır menü, select hello tooreplicate istediğiniz abonelik.
2. **Dağıtım modeli:** Select hello dağıtım modeli (Klasik veya Resource Manager)

Dağıtım modeli seçilen hello üzerinde bağlı olarak, bir doğrulama sanal makine için en az bir uyumlu depolama hesabı ve sanal ağ hello hedef abonelik tooreplicate ve yük devretme sahip tooensure çalıştırılır.

Merhaba doğrulamaları başarıyla tamamlandığında, Tamam toogo toohello sonraki adım'ı tıklatın.

Uyumlu Resource Manager depolama hesabı veya sanal ağ yok ya da daha fazla tooadd istersiniz, hello tıklayarak bunu yapabilirsiniz **+ depolama hesabı** veya **+ ağ** hello hello üstündeki düğmeleri Dikey.

## <a name="next-steps"></a>Sonraki adımlar
[Çoğaltma ayarlarını yapılandırın](./site-recovery-setup-replication-settings-vmware.md).
