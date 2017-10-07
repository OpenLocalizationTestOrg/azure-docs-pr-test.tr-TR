---
title: "Azure Site Recovery kullanarak Hyper-V tooAzure çoğaltmayı (System Center VMM ile) aaaReview hello önkoşulları | Microsoft Docs"
description: "Çoğaltma, yük devretme ve VMM Bulutları tooAzure, şirket içi Hyper-V sanal kurtarma Azure Site Recovery ile ayarlamak için hello önkoşulları açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>2. adım: Hyper-V (VMM ile) tooAzure çoğaltma hello önkoşullarını gözden geçirme

Gözden sonra hello [senaryo mimarisinin](vmm-to-azure-walkthrough-architecture.md), bu makale toomake hello dağıtımının önkoşulları anladığınızdan emin okuyun. 

## <a name="prerequisites-and-limitations"></a>Önkoşullar ve sınırlamalar

**Gereksinim** | **Ayrıntılar**
--- | ---
**Azure hesabı** | Bir [Microsoft Azure hesabınızın](http://azure.microsoft.com/) olması gerekir.
**Azure depolama alanı** | Bir Azure depolama hesabı toostore çoğaltılmış verileri gerekir.<br/><br/> Merhaba depolama hesabı hello olmalıdır hello aynı bölgede Azure kurtarma Hizmetleri kasası.<br/><br/>[Coğrafi olarak yedekli depolama](../storage/common/storage-redundancy.md#geo-redundant-storage) veya yerel olarak yedekli depolama kullanabilirsiniz. Coğrafi olarak yedekli depolama kullanmanızı öneririz. Coğrafi olarak yedekli depolama ile veri bölgesel bir kesinti oluşursa ya da hello birincil bölgenin kurtarılamaması esnektir.<br/><br/> Standart Azure depolama hesabı kullanabilir veya Azure [premium depolama](../storage/common/storage-premium-storage.md) kullanabilirsiniz. Premium depolama, G/Ç yoğun iş yüklerini destekler ve genellikle tutarlı bir şekilde yüksek G/Ç performansı ve düşük gecikme süresi gerektiren VM'ler için kullanılır. Çoğaltılan veriler için premium depolama kullanırsanız, ayrı bir standart depolama hesabı gerekir. Standart depolama hesabı sürekli değişikliklerin tooon içi verilerini yakalama çoğaltma günlükleri depolar.
**Azure ağı** | Gereksinim duyduğunuz bir [Azure ağ](../virtual-network/virtual-network-get-started-vnet-subnet.md), toowhich Azure Vm'lerinin yük devretme sonrasında bağlanın. Hello Azure ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.
**Şirket içi VMM sunucuları** | System Center 2012 R2 veya sonraki sürümlerini çalıştıran bir veya daha fazla VMM sunucunuzun olması gerekir.<br/><br/> Her VMM sunucusunun bir veya daha fazla özel bulutu olmalıdır. Her bulut bir veya birden fazla konak grubuna sahip olmalıdır.<br/><br/> Merhaba VMM sunucusunun Internet erişimi olmalıdır.
**Şirket içi Hyper-V** | Hyper-V ana bilgisayar sunucularının en az çalıştırmalıdır hello Hyper-V rolü etkin ya da Microsoft Hyper-V Server 2012 R2 ile Windows Server 2012 R2. Merhaba en son güncelleştirmelerin yüklü olmalıdır.<br/><br/> Merhaba Hyper-V Konağı (VMM bulutta bulunan) bir VMM konak grubunda yer almalıdır.<br/><br/> Bir konak tooreplicated istediğiniz bir veya daha fazla VM olması gerekir.<br/><br/> Hyper-V konakları bağlı toohello olmalıdır Internet çoğaltma tooAzure, doğrudan veya bir proxy ile. Hyper-V sunucuları makalesinde açıklanan hello düzeltmeler olmalıdır [2961977](https://support.microsoft.com/kb/2961977).
**Şirket içi Hyper-V VM'leri** | Tooreplicate çalışıyor istediğiniz sanal makineleri bir [işletim sistemi desteklenen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)ve uygun olması [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). Çoğaltma etkinleştirildikten sonra hello VM adı değiştirilebilir. 




## <a name="next-steps"></a>Sonraki adımlar

Çok Git[3. adım: kapasite planlama](vmm-to-azure-walkthrough-capacity.md)
