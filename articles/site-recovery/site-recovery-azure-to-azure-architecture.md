---
title: "Azure sanal makine çoğaltmasını Azure bölgeleri iş Azure Site kurtarma arasında aaaHow mu?  | Microsoft Belgeleri"
description: "Bu makalede, bileşenleri ve hello Azure Site Recovery hizmetini kullanarak Azure bölgeler arasında Azure sanal makineleri çoğaltırken kullanılan mimariye genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a>Azure VM çoğaltma Site Recovery nasıl çalışır?


Bu makalede hello bileşenleri ve süreçleri çoğaltılması ve Azure sanal makinelerini (VM'ler) kurtarma hello kullanarak tek bir bölge tooanother söz konusu [Azure Site Recovery](site-recovery-overview.md) hizmet.

>[!NOTE]
>Azure VM çoğaltma hello Site Recovery hizmeti ile şu anda önizlemede değil.

Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architectural-components"></a>Mimari bileşenler

Aşağıdaki diyagramda hello (Bu örnekte, Doğu ABD konumunda hello) belirli bir bölgede bir Azure VM ortamına üst düzey bir görünümünü sağlar. Bir Azure VM ortamda:
- Uygulamalar, diskleri depolama hesaplarında yayılan Vm'lerinde çalışıyor olabilir.
- bir sanal ağ içindeki bir veya daha fazla alt ağlarda Hello VM'ler dahil edilebilir.

![Müşteri ortamı](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Merhaba dağıtımının önkoşulları ve hello gereksinimleri hakkında bilgi edinin [destek matrisi](site-recovery-support-matrix-azure-to-azure.md).

## <a name="replication-process"></a>Çoğaltma işlemi

### <a name="step-1"></a>1. Adım

Hello Azure portalında Azure VM çoğaltmasında etkinleştirdiğinizde, aşağıdaki hello diyagramı ve tablo hello hedef bölgede otomatik olarak oluşturulan gösterilen kaynakları hello. Varsayılan olarak, kaynakları kaynak bölge ayarları temel alınarak oluşturulur. Merhaba hedef ayarları gerektiği gibi özelleştirebilirsiniz. [Daha fazla bilgi edinin](site-recovery-replicate-azure-to-azure.md).

![Çoğaltma işlemi, 1. adım etkinleştir](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

**Kaynak** | **Ayrıntılar**
--- | ---
**Hedef kaynak grubu** | Yük devretme sonrasında çoğaltılmış sanal makineleri ait kaynak grubu toowhich hello.
**Hedef sanal ağ** | Merhaba sanal ağ içinde çoğaltılmış VM'ler yük devretme sonrasında bulunur. Ağ eşlemesi, kaynak ve hedef sanal ağlar arasında ve tersi yönde oluşturulur.
**Önbellek depolama hesapları** | Kaynak VM'ler üzerindeki değişiklikler toohello hedef depolama hesabı çoğaltılan önce bunlar izlenen ve toohello önbellek depolama hesabı hello hedef konumda gönderilen. Bu VM hello üzerinde çalışan üretim uygulamalar üzerinde en az etki sağlar.
**Hedef depolama hesapları**  | Merhaba hedef konum toowhich hello verileri depolama hesaplarında çoğaltılır.
**Hedef kullanılabilirlik kümeleri**  | Kullanılabilirlik çoğaltılan hangi hello VM'ler yük devretme sonrasında bulunan ayarlar.

### <a name="step-2"></a>2. Adım

Çoğaltma etkin olarak hello Site Recovery uzantısı Mobility hizmeti hello VM üzerinde otomatik olarak yüklenir. Merhaba şunlar olur:

1. Merhaba VM Site Recovery ile kaydedilir.

2. Sürekli çoğaltma VM hello için yapılandırılır. Verileri yazar hello VM üzerinde disklerdir sürekli toohello önbellek depolama hesabı hello kaynak konumda aktarılan.

   ![Çoğaltma işlemi, 2. adım etkinleştir](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > Site kurtarma hiçbir zaman gelen bağlantı toohello VM gerekir. Merhaba VM yalnızca giden bağlantı tooSite kurtarma hizmeti URL'leri/IP adresleri, Office 365 kimlik doğrulaması URL'lerini/IP adresleri ve önbellek depolama hesabı IP adresi gerekiyor. Daha fazla bilgi için bkz: Merhaba [Azure sanal makineleri çoğaltmak için Ağ Kılavuzu](site-recovery-azure-to-azure-networking-guidance.md) makale.

## <a name="continuous-replication-process"></a>Sürekli çoğaltma işlemi

Sürekli çoğaltma çalışmaya başladıktan sonra disk yazma hemen olan toohello önbellek depolama hesabı aktarılan. Site Recovery hello verilerini işler ve toohello hedef depolama hesabı gönderir. Merhaba veri işlendikten sonra kurtarma noktaları birkaç dakikada hello hedef depolama hesabı oluşturulur.

## <a name="failover-process"></a>Yük devretme işlemi

Bir yük devretme başlatın, VM'ler oluşturulduktan hello hedef kaynak grubu, hedef sanal ağ, hedef alt hello ve hello kullanılabilirlik kümesi hedefleyin. Bir yük devretme sırasında herhangi bir kurtarma noktası kullanabilirsiniz.

![Yük devretme işlemi](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a>Sonraki adımlar

- Hakkında bilgi edinin [ağ](site-recovery-azure-to-azure-networking-guidance.md) Azure VM çoğaltması için.
- İzlenecek yollar çok izleyin[Azure Vm'lerini çoğaltma.](site-recovery-azure-to-azure.md)
