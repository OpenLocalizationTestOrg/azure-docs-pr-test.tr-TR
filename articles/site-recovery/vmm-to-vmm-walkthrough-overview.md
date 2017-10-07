---
title: aaaReplicate Hyper-V sanal makineleri tooa ikincil VMM sitesi Azure Site Recovery ile | Microsoft Docs
description: "Hello Azure portal kullanarak Hyper-V sanal makineleri tooa ikincil VMM sitesi çoğaltmak için genel bir bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Hyper-V sanal makineleri VMM Bulutları tooa ikincil VMM sitesi Çoğalt

> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-vmm-to-vmm.md)
> * [Klasik portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Bu makalede adımlar gerekli tooreplicate şirket içi Hyper-V sanal makineleri (VM'ler) tooa ikincil VMM konum, System Center Virtual Machine Manager (VMM) bulutlarında yönetilen hello genel bir bakış sağlar kullanarak [Azure Site Recovery](site-recovery-overview.md)hello Azure Portalı'nda.

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>1. adım: Gözden geçirme hello senaryo mimarisi

Dağıtımı başlatmak hello senaryo mimarisinin gözden geçirin ve tüm hello bileşenleri anladığınızdan emin olun toodeploy olması gerekir.

Çok Git[1. adım: gözden hello mimarisi](vmm-to-vmm-walkthrough-architecture.md).

## <a name="step-2-review-prerequisites-and-limitations"></a>2. adım: Gözden geçirme Önkoşullar ve sınırlamalar

Merhaba dağıtımının önkoşulları ve kısıtlamaları anladığınızdan emin olun.

**Azure önkoşulları**: Microsoft Azure aboneliğinizin olması gerekir ve Azure kurtarma Hizmetleri kasası, tooorchestrate ve çoğaltmayı yönetme.
**Şirket içi VMM sunucuları ve Hyper-V konakları**: VMM sunucuları ve Hyper-V konakları uyumlu ve Site Recovery dağıtımı için hazır olduğundan emin olun.

Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](vmm-to-vmm-walkthrough-prerequisites.md).

## <a name="step-3-plan-networking"></a>3. adım: ağ planlama

Merhaba senaryo dağıttığınızda VMM VM ağları arasında ağ eşlemesi yapılandırabilirsiniz tooensure planlama bazı ağ toodo gerekir.

Çok Git[3. adım: ağ planlama](vmm-to-vmm-walkthrough-network.md).


## <a name="step-4-prepare-vmm-and-hyper-v"></a>4. adım: VMM ve Hyper-V hazırlama

Merhaba VMM sunucuları ve Hyper-V konakları Site Recovery dağıtımı için hazırlayın.

Çok Git[4. adım: şirket içi sunucuları hazırlama](vmm-to-vmm-walkthrough-vmm-hyper-v.md).

## <a name="step-5-set-up-a-vault"></a>5. adım: Bir kasa ayarlama

Kurtarma Hizmetleri kasasını ayarlayın. Merhaba kasası yapılandırma ayarlarını içeren, çoğaltma ve yönetir.

[5. adım: bir kasasını oluşturup](vmm-to-vmm-walkthrough-create-vault.md).

## <a name="step-6-set-up-source-and-target-settings"></a>6. adım: kaynak ve hedef ayarlarını belirleme

Merhaba kaynak ve hedef çoğaltma VMM konumları ayarlama. Merhaba VMM sunucuları toohello kasası ekleyin ve Site Recovery bileşenlerini hello yükleme dosyalarını indirin. Merhaba VMM sunucusunda Azure Site kurtarma sağlayıcısı kurulumunu çalıştırın. Kurulum hello VMM sunucusunda sağlayıcı hello yükler ve hello sunucu hello kasasına kaydeder. Her Hyper-V ana bilgisayarda hello Microsoft Kurtarma Hizmetleri aracısını yükleyin.

Çok Git[adım 6: hello kaynak ve hedef ayarlar](vmm-to-vmm-walkthrough-source-target.md).

## <a name="step-7-configure-network-mapping"></a>7. Adım: Ağ eşlemesini yapılandırma

Merhaba kaynak ve hedef konumların VMM VM ağlarında eşleyin. Yük devretme sonrasında VM'ler hello hedef ağ hangi hello kaynak Hyper-V VM bulunduğu eşlemeleri toohello kaynak bir VM ağı oluşturulur.

Çok Git[adım 7: ağ eşlemesini yapılandırma](vmm-to-vmm-walkthrough-network-mapping.md).


## <a name="step-8-set-up-a-replication-policy"></a>8. adım: Bir çoğaltma ilkesi ayarlama

Sanal makineleri VMM konumlar arasında nasıl çoğaltılır belirtin.

Çok Git[adım 8: bir çoğaltma ilkesini ayarlayın](vmm-to-vmm-walkthrough-replication.md).


## <a name="step-9-enable-replication-for-vms"></a>9. adım: sanal makineleri için çoğaltmayı etkinleştirme

Tooreplicate istediğiniz hello sanal makineleri seçin. Çoğaltma Tetikleyicileri hello ilk çoğaltma toohello ikincil site için bir VM etkinleştirildikten sonra devam eden değişim çoğaltması tarafından kullanılıyordu.

Çok Git[adım 9: çoğaltmasını etkinleştir](vmm-to-vmm-walkthrough-enable-replication.md).


## <a name="step-10-run-a-test-failover"></a>10. adım: yük devretme testi çalıştırma

Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.

Çok Git[adım 10: bir yük devretme testi](vmm-to-vmm-walkthrough-test-failover.md).
