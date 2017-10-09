---
title: "Hyper-V çoğaltma tooa ikincil VMM sitesi Azure Site Recovery ile aaaReview hello önkoşulları | Microsoft Docs"
description: "Hyper-V sanal makineleri tooa Azure Site Recovery ile ikincil VMM sitesi çoğaltılması hello önkoşulları açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>2. adım: Gözden geçirme hello için Önkoşullar ve sınırlamalar Hyper-V VM çoğaltma tooa ikincil VMM sitesi


Merhaba gözden geçirdikten sonra [senaryo mimarisinin](vmm-to-vmm-walkthrough-architecture.md), şirket içi Hyper-V sanal makineleri (VM'ler) çoğaltma Sistem Merkezi sanal yönetildiğinde hello dağıtımının önkoşulları anladığınızdan emin Bu makale toomake okuma Machine Manager (VMM) bulut, ikincil tooa kullanarak site [Azure Site Recovery](site-recovery-overview.md) hello Azure Portalı'nda.

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites-and-limitations"></a>Önkoşullar ve sınırlamalar

**Gereksinim** | **Ayrıntılar**
--- | ---
**Azure** | A [Microsoft Azure](http://azure.microsoft.com/) abonelik.<br/><br/> [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.<br/><br/> Site Recovery fiyatlandırması hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/details/site-recovery/).<br/><br/> Site Recovery, altında coğrafi kullanılabilirlik kısmına hello desteklenen bölgeleri kontrol [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
**VMM sunucuları** | İki VMM sunucusu, bir hello birincil sitedeki ve hello ikincil birinde olması önerilir.<br/><br/> Tek bir Bulutlar arasında çoğaltma VMM sunucusunda desteklenir.<br/><br/> VMM sunucuları çalışıyor. en az hello en son güncelleştirmeleri içeren System Center 2012 SP1.<br/><br/> VMM sunucuları Internet erişimine gerek vardır.
**VMM Bulutları** | Her bir VMM sunucusunun bir veya daha fazla bulut olmalıdır ve tüm Bulutlar hello Hyper-V Kapasite profili kümesine sahip olması gerekir. <br/><br/>Bulut bir veya daha fazla VMM ana bilgisayar grubu içermesi gerekir.<br/><br/> Yalnızca bir VMM sunucunuz varsa, en az iki bulut, tooact olarak birincil ve ikincil gerekir.
**Hyper-V** | Hyper-V sunucuları çalışıyor olmalıdır en az Windows Server 2012 hello Hyper-V rolüne sahip ve hello son güncelleştirmelerin yüklü olması.<br/><br/> Bir Hyper-V sunucusunun bir veya daha fazla VM içermesi gerekir.<br/><br/>  Hyper-V ana bilgisayar sunucuları konak grupları hello birincil ve ikincil VMM bulutlarında yer.<br/><br/> Windows Server 2012 R2'de bir kümede Hyper-V çalıştırırsanız, yükleme [2961977 güncelleştir](https://support.microsoft.com/kb/2961977)<br/><br/> Windows Server 2012'de bir kümede Hyper-V çalıştırırsanız, bir statik IP adresi tabanlı kümeniz varsa küme aracısının otomatik olarak oluşturulmaz. Merhaba küme aracısını el ile yapılandırın. [Daha fazla bilgi edinin](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Hyper-V sunucuları Internet erişimine gerek vardır.




## <a name="next-steps"></a>Sonraki adımlar

Çok Git[3. adım: ağ planlama](vmm-to-vmm-walkthrough-network.md).
