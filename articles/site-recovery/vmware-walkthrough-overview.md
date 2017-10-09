---
title: Azure Site Recovery ile aaaReplicate VMware Vm'lerini tooAzure | Microsoft Docs
description: "VMware Vm'leri tooAzure üzerinde çalışan iş yüklerini çoğaltmak için hello adımlara genel bir bakış sağlar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>Site Recovery ile VMware Vm'lerini tooAzure Çoğalt

Bu makalede hello kullanarak hello adımları gerekli tooreplicate şirket içi VMware sanal makineleri tooAzure, genel bir bakış sağlar [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.


![Dağıtım işlemi](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**Şekil 1: Dağıtım işlemi özeti**

## <a name="step-1-review-architecture-and-prerequisites"></a>1. adım: mimarisi ve önkoşulları gözden geçirin

Dağıtıma başlamadan önce hello senaryo mimarisinin gözden geçirin ve toodeploy gerek duyduğunuz tüm hello bileşenleri anladığınızdan emin olun

Çok Git[1. adım: gözden hello mimarisi](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>2. adım: Gözden geçirme önkoşulları

Merhaba Önkoşullar her dağıtım bileşen için yerinde olduğundan emin olun:

- **Azure önkoşulları**: bir Microsoft Azure hesabı, Azure ağları ve depolama hesapları gerekir.
- **Şirket içi Site Recovery bileşenlerini**: şirket içi Site Recovery bileşenlerini çalıştıran bir makineye gerekir.
- **Şirket içi VMware Önkoşullar**: Site Recovery VMware sunucularını ve Vm'leri erişebilmesi için hesaplarını tooset gerekir.
- **Çoğaltılan VM'ler**: tooreplicate gerek toocomply Azure gereksinimleri ile istediğiniz ve hello Mobility hizmeti bileşeninin yüklü olan VM'ler.

Çok Git[2. adım: gözden Önkoşullar ve sınırlamalar](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>3. adım: Planı kapasite

Tam dağıtımını yaptığınız ihtiyacınız hangi çoğaltma kaynakları çıkışı toofigure gerekir. Birkaç vardır Araçlar kullanılabilir toohelp bunu. TooStep 2 gidin. Tootest hello ortamını ayarlama hızlı yaptığınız varsa bu adımı atlayabilirsiniz.

Çok Git[3. adım: kapasite planlama](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>4. adım: ağ planlama

Yük devretme gerçekleştikten sonra Azure Vm'lerinin bağlı toonetworks olduğunu ve sahip oldukları hello doğru IP adreslerine tooensure planlama bazı ağ toodo gerekir.

Çok Git[4. adım: ağ planı](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>5. adım: Azure kaynaklarını hazırlama

Başlamadan önce Azure ağları ve depolama ayarlayın. Dağıtım sırasında bunu yapabilirsiniz ancak başlamadan önce bunu öneririz.

Çok Git[5. adım: Azure hazırlama](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>6. adım: VMware hazırlama

Site Recovery için kullanacağı hesaplarını tooset gerekir:

- Erişim VMware sanallaştırma sunucuları tooautomatically VM'ler algıla.
- Sanal makineleri tooinstall hello Mobility hizmeti erişin. Tooreplicate hello Mobility Hizmeti Aracısı önce yüklü olması gerekir istediğiniz her bir VM çoğaltmayı etkinleştirebilirsiniz.

Çok Git[adım 6: VMware hazırlama](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>7. adım: Bir kasa ayarlama

Çoğaltmayı yönetmek ve bir kurtarma Hizmetleri kasası tooorchestrate yukarı tooset gerekir. Merhaba kasasını ayarladığınızda, istediğinizi belirtin tooreplicate, ve tooreplicate istediğiniz şekilde.

Çok Git[adım 7: bir kasasını oluşturup](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>8. adım: kaynak ve hedef ayarlarını yapılandırma

Merhaba kaynak ve çoğaltma için kullanılan hedef ayarlayın. Kaynak ayarları ayarı birleşik Kurulum tooinstall hello şirket içi Site Recovery bileşenlerini çalıştıran içerir.

Çok Git[adım 8: hello kaynak ve hedef ayarlama](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>9. adım: Bir çoğaltma ilkesi ayarlama

Merhaba kasasına VMware Vm'leri için bir ilke toospecify çoğaltma ayarlarını belirleme.

Çok Git[adım 9: bir çoğaltma ilkesini ayarlayın](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>10. adım: hello Mobility hizmetini yükleme

Merhaba mobilite hizmetinin yüklenmesi tooreplicate istediğiniz her VM. Birkaç yolu tooset iterek ister çekerek yükleme hello hizmetiyle yukarı vardır.

Çok Git[adım 10: hello Mobility hizmetini yükleme](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>11. adım: Çoğaltma etkinleştirme

Merhaba Mobility hizmeti bir VM üzerinde çalışmaya başladıktan sonra çoğaltmayı etkinleştirebilirsiniz. Etkinleştirdikten sonra ilk çoğaltma işlemi hello VM oluşur.

Çok Git[adım 11: çoğaltmasını etkinleştir](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>12. adım: yük devretme testi çalıştırma

İlk çoğaltma sonlandırıldıktan ve değişim çoğaltması çalıştıran sonra her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırabilirsiniz.

Çok Git[adım 12: yük devretme testi çalıştırma](vmware-walkthrough-test-failover.md)
