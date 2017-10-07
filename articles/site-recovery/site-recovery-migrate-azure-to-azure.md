---
title: "Azure bölgeler arasında Azure Iaas Vm'leri aaaMigrate | Microsoft Docs"
description: "Azure Site Recovery toomigrate Azure Iaas sanal makineleri bir Azure bölgesi tooanother kullanın."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Azure Site Recovery ile Azure bölgeler arasında Azure Iaas sanal makineleri geçirme
## <a name="overview"></a>Genel Bakış
Site Recovery tooAzure Hoş Geldiniz! Bu makalede, Azure bölgeler arasında toomigrate Azure VM'ler istiyorsanız kullanın. Başlamadan önce dikkat edin:

* Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeline sahiptir: Azure Resource Manager ve klasik. Ayrıca Azure iki portala – hello Klasik dağıtım modelini destekleyen Klasik Azure portalı hello ve her iki dağıtım modeline de destek Azure portal hello sahiptir. geçiş için Kaynak Yöneticisi'nde veya Klasik Site Recovery yapılandırmakta olup olmadığını hello temel adımlar aynı hello. Ancak kullanıcı Arabirimi yönergeleri hello ve ekran görüntüleri bu makalede Azure portal hello için ilgilidir.
* **Şu anda yalnızca tek bir bölge tooanother geçirebilirsiniz. Bir Azure bölgesi tooanother VM'ler başarısız olabilir, ancak siz bunları geri yeniden kapatamazsınız.**

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Ön koşullar
İşte bu dağıtım için gerekenler:

* **Iaas sanal makineleri**: toomigrate istediğiniz sanal makineleri hello. Bu sanal makineleri fiziksel makineleri düşünerek geçirin.

## <a name="deployment-steps"></a>Dağıtım adımları
Bu bölümde hello yeni Azure portalında hello dağıtım adımları açıklanmaktadır.

1. [Bir kasa oluşturun](site-recovery-vmware-to-azure.md).
2. [Çoğaltmayı etkinleştirme](site-recovery-vmware-to-azure.md). Merhaba toomigrate istediğiniz ve Azure kaynağı olarak seçin VM'ler çoğaltmayı etkinleştirin. 
3. [Planlanmamış bir yük devretme çalıştırmak](site-recovery-failover.md). İlk çoğaltma tamamlandıktan sonra planlanmamış bir yük devretme bir Azure bölgesi tooanother çalıştırabilirsiniz. İsteğe bağlı olarak, bir kurtarma planı oluşturun ve bölgeler arasında birden çok sanal makine planlanmamış yük devretme, toomigrate çalıştırın. [Daha fazla bilgi edinin](site-recovery-create-recovery-plans.md) kurtarma planları hakkında.

## <a name="next-steps"></a>Sonraki adımlar
Diğer çoğaltma senaryolarda hakkında daha fazla bilgi [Azure Site Recovery nedir?](site-recovery-overview.md)
