---
title: "aaaInstall hello VMware tooAzure çoğaltma için Mobility hizmetini | Microsoft Docs"
description: "Bu makalede nasıl Mobility Hizmeti Aracısı VMware tooAzure çoğaltma hello Azure Site Recovery hizmeti ile Merhaba tooinstall açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>10. adım: hello Mobility hizmetini yükleme


Bu makalede nasıl çoğaltırken tooconfigure kaynak ve hedef ayarları şirket içi VMware sanal makineleri tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

Merhaba Mobility hizmeti bir makinede veri Yazar yakalar ve bunları toohello işlem sunucusuna iletir. Tooreplicate tooAzure istediğiniz her makinede yüklenmelidir.

Çoğaltma etkin olduğunda hello Site kurtarma işlemi sunucusundan bir anında yükleme kullanarak hello Mobility hizmeti el ile yükleyin veya System Center Configuration Manager aracını kullanın. Anında yükleme kullanırsanız, çoğaltma etkin olduğunda hello hizmeti hello VM üzerinde yüklendi.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>El ile yükleme

1. Merhaba denetleyin [Önkoşullar](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) el ile yükleme.
2. İzleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) hello portal'ı kullanarak el ile yükleme.
3. Merhaba komut satırından tooinstall tercih ederseniz, izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Merhaba işlem sunucusundan yükle

Bir sanal makine için çoğaltmayı etkinleştirdiğinizde toopush hello Mobility hizmeti yüklemesi hello işlem sunucusundan istiyorsanız, hello işlem sunucusu tooaccess hello VM tarafından kullanılan bir hesabınızın olması gerekir. Merhaba hesabı yalnızca hello gönderme yüklemesi için kullanılır.

1. Olması [hesap oluşturup](vmware-walkthrough-prepare-vmware.md) gönderme yüklemesi için kullanılabilir. Ardından, Site Recovery dağıtımı sırasında kaynak ayarlarını yapılandırırken toouse istediğiniz hello hesabının de belirtin.
2. Ardından izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) toopush hello Mobility hizmeti Windows veya Linux çalıştıran sanal makineleri üzerinde istiyorsanız.

## <a name="other-methods"></a>Diğer yöntemleri

Daha fazla bilgi edinmek [hello Mobility hizmetinin Yapılandırma Yöneticisi'ni kullanarak yükleme](site-recovery-install-mobility-service-using-sccm.md), veya kullanarak [Azure Otomasyonu DSC](site-recovery-automate-mobility-service-install.md).

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 11: çoğaltmasını etkinleştir](vmware-walkthrough-enable-replication.md)
