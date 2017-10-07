---
title: vmm'de Hyper-V sanal makineleri aaaReplicate bulut Azure Site Recovery ile tooAzure | Microsoft Docs
description: "VMM Bulutları tooAzure hello Azure Site Recovery hizmetini kullanarak Hyper-V sanal makineleri çoğaltmak için genel bir bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>VMM Bulutları tooAzure hello Azure portalında Site Recovery kullanarak Hyper-V sanal makineleri Çoğalt
> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-vmm-to-azure.md)
> * [Azure klasik](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell klasik](site-recovery-deploy-with-powershell.md)


Bu makalede hello adımları gerekli tooreplicate genel bir bakış şirket içi Hyper-V sanal makineleri (VM'ler) System Center Virtual Machine Manager (VMM) Bulutlar tooAzure hello kullanarak yönetilen sağlar [Azure Site Recovery](site-recovery-overview.md) hizmeti Hello Azure portalı.

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>1. adım: Gözden geçirme hello senaryo mimarisi

Dağıtımı başlatmak hello senaryo mimarisinin gözden geçirin ve tüm hello bileşenleri anladığınızdan emin olun toodeploy olması gerekir.

Çok Git[1. adım: gözden hello mimarisi](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>2. adım: Gözden geçirme Önkoşullar ve sınırlamalar

Merhaba dağıtımının önkoşulları ve kısıtlamaları anladığınızdan emin olun.

**Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.
**Şirket içi VMM sunucuları ve Hyper-V konakları**: VMM sunucuları ve Hyper-V konakları uyumlu ve Site Recovery dağıtımı için hazır olduğundan emin olun.
**Çoğaltılan VM'ler**: tooreplicate istediğiniz sanal makineleri Azure gereksinimlerine uymak denetleyin.

Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>3. adım: Planı kapasite

Tam dağıtımını yaptığınız, ihtiyacınız hangi çoğaltma kaynakları çıkışı toofigure gerekir. Birkaç vardır Araçlar kullanılabilir toohelp bunu. Tootest hello ortamını ayarlama hızlı yaptığınız varsa, bu adımı atlayabilirsiniz.

Çok Git[3. adım: kapasite planlama](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>4. adım: ağ planlama

Azure VM'ler bağlı tooAzure sanal ağları yük devretme gerçekleştikten sonra uygun IP atanmış oldukları adresleri olacaktır toodo hello senaryo dağıttığınızda ağ eşlemesi yapılandırabilirsiniz tooensure planlama bazı ağ gerekir.

Çok Git[4. adım: ağ planı](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>5. adım: Azure kaynaklarını hazırlama

Bir Azure hesabı, ağlara ve depolama ayarlayın. Dağıtım sırasında bunu yapabilirsiniz ancak başlamadan önce bunu öneririz.

Çok Git[5. adım: Azure hazırlama](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>6. adım: VMM ve Hyper-V hazırlama

Merhaba şirket içi VMM sunucuları ve Hyper-V konakları Site Recovery dağıtımı için hazırlayın.

Çok Git[6. adım: şirket içi sunucuları hazırlama](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>7. adım: Bir kasa ayarlama

Kurtarma Hizmetleri kasasını ayarlayın. Merhaba kasası yapılandırma ayarlarını içeren, çoğaltma ve yönetir.

[7. adım: Bir kasa ayarlama](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>8. adım: kaynak ve hedef ayarlarını yapılandırma

Merhaba kaynak ve hedef çoğaltma konumları ayarlama. Merhaba VMM server toohello kasası ekleyin ve Site Recovery bileşenlerini hello yükleme dosyalarını indirin. Merhaba VMM sunucusunda Azure Site kurtarma sağlayıcısı kurulumunu çalıştırın. Kurulum hello VMM sunucusunda sağlayıcı hello yükler ve hello sunucu hello kasasına kaydeder. Her Hyper-V ana bilgisayarda hello Microsoft Kurtarma Hizmetleri aracısını yükleyin.

Çok Git[adım 8: kaynak ve hedef ayarlarını yapılandırma](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>9. adım: ağ eşlemesini yapılandırma

Harita VMM VM ağları tooAzure sanal ağlar şirket içi. Yük devretme sonrasında Azure Vm'lerinin hello hangi hello kaynak Hyper-V bulunduğu toohello şirket içi VM ağ eşlemeleri Azure ağı oluşturulur.

Çok Git[adım 9: ağ eşlemesini yapılandırma](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>10. adım: Bir çoğaltma ilkesi ayarlama

Şirket içi sanal makineleri çoğaltılmış tooAzure ne olacağını belirtin.

Çok Git[adım 10: bir çoğaltma ilkesini ayarlayın](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>11. adım: sanal makineleri için çoğaltmayı etkinleştirme

Tooreplicate istediğiniz hello sanal makineleri seçin. Bir VM için çoğaltma Tetikleyicileri hello ilk çoğaltma tooAzure etkinleştirildikten sonra devam eden değişim çoğaltması tarafından kullanılıyordu.

Çok Git[adım 11: çoğaltmasını etkinleştir](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>12. adım: yük devretme testi çalıştırma

Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.

Çok Git[adım 12: yük devretme testi çalıştırma](vmm-to-azure-walkthrough-test-failover.md)


