---
title: "Azure bölgeler arasında Azure VM'ler, çoğaltma için aaaReview hello mimarisi | Microsoft Docs"
description: "Bu makalede, bileşenleri ve Azure Vm'leri hello Azure Site Recovery hizmetini kullanarak Azure bölgeler arasında çoğaltırken kullanılan mimariye genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a>1. adım: Azure bölgeler arasında Azure VM çoğaltması için hello mimarisi gözden geçirin


Merhaba gözden geçirdikten sonra [genel bakış adımları](azure-to-azure-walkthrough-overview.md) bu dağıtım için bu makale toounderstand hello bileşenleri ve süreçleri çoğaltılması ve Azure sanal makineleri (VM'ler) bir Azure bölgesi tooanother, Kurtarma sırasında kullanılan okuma kullanma [Azure Site Recovery](site-recovery-overview.md).

- Merhaba makale bitirdikten sonra Azure VM çoğaltma tooanother bölge nasıl çalıştığını anlamak olmalıdır.
- Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>Azure VM çoğaltma hello Site Recovery hizmeti ile şu anda önizlemede değil.



## <a name="architectural-components"></a>Mimari bileşenler

Aşağıdaki diyagramda hello (Bu örnekte, Doğu ABD konumunda hello) belirli bir bölgede bir Azure VM ortamına üst düzey bir görünümünü sağlar. Bir Azure VM ortamda:
- Uygulamalar, diskleri depolama hesaplarında yayılan Vm'lerinde çalışıyor olabilir.
- bir sanal ağ içindeki bir veya daha fazla alt ağlarda Hello VM'ler dahil edilebilir.

![Müşteri ortamı](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a>Çoğaltma işlemi

### <a name="step-1"></a>1. Adım

Hello Azure portalında Azure VM çoğaltmasında etkinleştirdiğinizde, aşağıdaki hello diyagramı ve tablo hello hedef bölgede otomatik olarak oluşturulan gösterilen kaynakları hello. Varsayılan olarak, kaynakları kaynak bölge ayarları temel alınarak oluşturulur. Merhaba hedef ayarları gerektiği gibi özelleştirebilirsiniz. [Daha fazla bilgi edinin](site-recovery-replicate-azure-to-azure.md).

![Çoğaltma işlemi, 1. adım etkinleştir](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

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

   ![Çoğaltma işlemi, 2. adım etkinleştir](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  Site Recovery hiç bağlantı toohello VM gelen gerektiğini unutmayın. Yalnızca bağlantı tooSite kurtarma hizmeti URL'leri/IP adresleri, Office 365 kimlik doğrulaması URL'lerini/IP adresleri ve önbellek depolama hesabı IP adresleri gerekli giden. 

## <a name="continuous-replication-process"></a>Sürekli çoğaltma işlemi

Sürekli çoğaltma çalışmaya başladıktan sonra disk yazma hemen olan toohello önbellek depolama hesabı aktarılan. Site Recovery hello verilerini işler ve toohello hedef depolama hesabı gönderir. Merhaba veri işlendikten sonra kurtarma noktaları birkaç dakikada hello hedef depolama hesabı oluşturulur.

## <a name="failover-process"></a>Yük devretme işlemi

Bir yük devretme başlatın, VM'ler oluşturulduktan hello hedef kaynak grubu, hedef sanal ağ, hedef alt hello ve hello kullanılabilirlik kümesi hedefleyin. Bir yük devretme sırasında herhangi bir kurtarma noktası kullanabilirsiniz.

![Yük devretme işlemi](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](azure-to-azure-walkthrough-prerequisites.md)
