---
title: "Azure bölgeler arasında Azure Iaas Vm'leri geçirme | Microsoft Docs"
description: "Azure Iaas sanal makineleri bir Azure bölgesinden diğerine geçirmek için Azure Site Recovery kullanın."
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
ms.openlocfilehash: ef2972c077a2b1dd2b2fd6ce53cc6560520ea870
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Azure Site Recovery ile Azure bölgeler arasında Azure Iaas sanal makineleri geçirme
## <a name="overview"></a>Genel Bakış
Azure Site Recovery'ye hoş geldiniz! Azure VM'ler Azure bölgeler arasında geçirmek istiyorsanız bu makaleyi kullanın. Başlamadan önce dikkat edin:

* Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeline sahiptir: Azure Resource Manager ve klasik. Ayrıca Azure iki portala sahiptir: Klasik dağıtım modelini destekleyen klasik Azure portalı ve her iki dağıtım modeline de destek sağlayan Azure portalı. Site Recovery Kaynak Yöneticisi'nde veya Klasik yapılandırmakta olup olmadığını geçiş için temel adımlar aynıdır. Ancak kullanıcı Arabirimi yönergeleri ve ekran görüntüleri bu makalede Azure portal ilgilidir.
* **Şu anda yalnızca bir bölgesinden diğerine geçirebilirsiniz. Bir Azure bölgesinden Vm'lere devredebildiğini, ancak siz bunları geri yeniden kapatamazsınız.**

Tüm yorumlarınızı ve sorularınızı bu makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar
İşte bu dağıtım için gerekenler:

* **Iaas sanal makineleri**: geçiş yapmak istediğiniz sanal makineleri. Bu sanal makineleri fiziksel makineleri düşünerek geçirin.

## <a name="deployment-steps"></a>Dağıtım adımları
Bu bölümde, yeni Azure portalında dağıtım adımları açıklanmaktadır.

1. [Bir kasa oluşturun](site-recovery-vmware-to-azure.md).
2. [Çoğaltmayı etkinleştirme](site-recovery-vmware-to-azure.md). Geçirmek istediğiniz VM'ler için çoğaltmayı etkinleştirmek ve Azure kaynağı olarak seçin. 
3. [Planlanmamış bir yük devretme çalıştırmak](site-recovery-failover.md). İlk çoğaltma tamamlandıktan sonra planlanmamış bir yük devretme bir Azure bölgesinden diğerine çalıştırabilirsiniz. İsteğe bağlı olarak, bir kurtarma planı oluşturmak ve birden çok sanal makine bölgeler arasında geçirmek için planlanmamış yük devretme, çalıştırın. [Daha fazla bilgi edinin](site-recovery-create-recovery-plans.md) kurtarma planları hakkında.

## <a name="next-steps"></a>Sonraki adımlar
Diğer çoğaltma senaryolarda hakkında daha fazla bilgi [Azure Site Recovery nedir?](site-recovery-overview.md)
