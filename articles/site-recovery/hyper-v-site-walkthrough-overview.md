---
title: Azure Site Recovery ile aaaReplicate Hyper-V sanal makineleri tooAzure | Microsoft Docs
description: "Açıklar nasıl tooorchestrate çoğaltma, yük devretme ve kurtarma işlemlerini şirket içi Hyper-V sanal makineleri tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>Hyper-V sanal makineleri (VMM olmadan) tooAzure Çoğalt 

> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-hyper-v-site-to-azure.md)
> * [Azure klasik](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Bu makalede hello kullanarak hello gerekli adımları tooreplicate şirket içi Hyper-V sanal makineleri tooAzure, genel bir bakış sağlar [Azure Site Recovery](site-recovery-overview.md) hello Azure Portalı'nda. Bu dağıtım Hyper-V VM System Center Virtual Machine Manager (VMM) tarafından yönetilmiyor.


Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-architecture-and-prerequisites"></a>1. adım: mimarisi ve önkoşulları gözden geçirin

Dağıtıma başlamadan önce hello senaryo mimarisinin gözden geçirin ve toodeploy gerek duyduğunuz tüm hello bileşenleri anladığınızdan emin olun

Çok Git[1. adım: gözden hello mimarisi](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>2. adım: Gözden geçirme önkoşulları

Merhaba Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:

- **Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.
- **Şirket içi Hyper-V önkoşulları**: Hyper-V konakları Site Recovery dağıtımı için hazır olduğundan emin olun.
- **Çoğaltılan VM'ler**: istediğiniz tooreplicate gerek toocomply Azure gereksinimleri olan VM'ler.

Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>3. adım: Planı kapasite

Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları çıkışı toofigure gerekir. Birkaç vardır Araçlar kullanılabilir toohelp bunu. TooStep 2 gidin. Tootest hello ortamını ayarlama hızlı yaptığınız varsa bu adımı atlayabilirsiniz.

Çok Git[3. adım: kapasite planlama](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>4. adım: ağ planlama

Yük devretme gerçekleştikten sonra Azure Vm'lerinin bağlı toonetworks olduğunu ve sahip oldukları hello doğru IP adreslerine tooensure planlama bazı ağ toodo gerekir.

Çok Git[4. adım: ağ planı](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>5. adım: Azure kaynaklarını hazırlama

Başlamadan önce Azure ağları ve depolama ayarlayın. Dağıtım sırasında bunu yapabilirsiniz ancak başlamadan önce bunu öneririz.

Çok Git[5. adım: Azure hazırlama](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>6. adım: Hyper-V hazırlama

Hyper-V sunucuları Site Recovery dağıtım gereksinimleri karşıladığından emin olun.

Çok Git[adım 6: Hyper-V hazırlama](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>7. adım: Bir kasa ayarlama

Çoğaltmayı yönetmek ve bir kurtarma Hizmetleri kasası tooorchestrate yukarı tooset gerekir. Merhaba kasasını ayarladığınızda, istediğinizi belirtin tooreplicate, ve tooreplicate istediğiniz şekilde.

Çok Git[adım 7: bir kasa oluşturun](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>8. adım: kaynak ve hedef ayarlarını yapılandırma

Merhaba kaynak ve çoğaltma için kullanılan hedef ayarlayın. Kaynak ayarları ayarı, her Hyper-V ana bilgisayarda hello Site Recovery sağlayıcısı ve kurtarma Hizmetleri aracısını yükleme ve hello site kurtarma Hizmetleri kasası hello kaydetme Hyper-V konakları tooa Hyper-V sitesi eklemeyi içerir.

Çok Git[adım 8: hello kaynak ve hedef ayarlama](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>9. adım: Bir çoğaltma ilkesi ayarlama

Merhaba kasasına Hyper-V VM'ler için bir ilke toospecify çoğaltma ayarlarını belirleme.

Çok Git[adım 9: bir çoğaltma ilkesini ayarlayın](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>10. adım: Çoğaltma etkinleştirme

Etkinleştirdikten sonra yerinde bir çoğaltma ilkesi oluşturduktan sonra ilk çoğaltmasının hello VM oluşur.

Çok Git[adım 10: çoğaltmasını etkinleştir](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>11. adım: yük devretme testi çalıştırma

İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırabilirsiniz.

Çok Git[11. adım: yük devretme testi çalıştırma](hyper-v-site-walkthrough-test-failover.md)
