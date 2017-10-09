---
title: "aaaRecovery Hizmetleri kasası ile ilgili SSS | Microsoft Docs"
description: "Bu sürümü hello SSS hello Azure Backup hizmeti hello genel önizleme sürümünü destekler. Yanıtlar toofrequently hakkında hello Yedekleme aracısı, yedekleme ve bekletme, Kurtarma, güvenlik ve diğer hello Azure Backup çözümü hakkında sık sorulan sorular."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "yedekleme çözümü; backup hizmeti"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>Kurtarma Hizmetleri kasası - SSS
Bu makalede bilgiler belirli tooRecovery Hizmetleri kasası sağlar ve hello tamamlayan [Azure yedekleme ile ilgili SSS](backup-azure-backup-faq.md). Hello Azure yedekleme ile ilgili SSS hello Azure Backup hizmeti hakkında sorular ve yanıtlar hello tam kümesi sağlar.  

Merhaba, bu makalenin veya ilgili bir makalenin Disqus bölümünde Azure yedekleme hakkında sorular sorabilirsiniz. Hello Azure Backup hizmeti hakkında sorular hello nakledebilirsiniz [tartışma Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Kurtarma Hizmetleri kasaları Resource Manager tabanlıdır. Backup kasaları (Klasik mod) hala destekleniyor mu? <br/>
Evet, Yedekleme kasaları hâlâ destekleniyor. Hello yedekleme kasaları oluşturun [Klasik portal](https://manage.windowsazure.com). Kurtarma Hizmetleri kasalarının hello oluşturma [Azure portal](https://portal.azure.com). Ancak, toocreate kurtarma Hizmetleri kasası tüm gelecekteki geliştirmeleri tavsiye yalnızca kurtarma Hizmetleri kasasına kullanılabilir olacaktır.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Bir yedekleme kasası tooa kurtarma Hizmetleri kasasına geçişini sağlayabilir miyim? <br/>
Ne yazık ki Hayır, şu anda, Kurtarma Hizmetleri kasası bir yedekleme kasası tooa Merhaba içeriğine geçiremezsiniz. Bu işlevi eklemeye yönelik çalışmalarımız devam ediyor ancak işlev Genel Önizleme kapsamında sunulmuyor.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Kurtarma Hizmetleri kasaları, klasik VM’leri mi Resource Manager tabanlı VM’leri mi destekler? <br/>
Kurtarma Hizmetleri kasaları iki modeli de destekler.  (Klasik mod Vm'lerini olan) hello Klasik portalda oluşturulan bir VM'yi yedekleyebilir veya VM hello (Resource Manager temelli olan) Azure portalında oluşturulan tooa kurtarma Hizmetleri kasası.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>Klasik VM’lerimi yedekleme kasasında yedekledim. Şimdi toomigrate Vm'lerimin Klasik modda tooResource Yöneticisi modundan istiyorum.  Bunları nasıl kurtarma hizmetleri kasasında yedekleyebilirim?
Hello sanal makineleri Klasik tooResource Yöneticisi modu Klasik sanal makineleri yedekleme kasasında yedeklerini otomatik olarak toorecovery Hizmetleri kasası geçirirken olmaz. VM yedeklerinin geçirilmesi için lütfen bu adımları izleyin:

1. Yedekleme kasasında çok Git**korunan öğeler** sekmesinde ve hello VM seçin. [Korumayı Durdur](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)’a tıklayın. *İlişkili yedekleme verilerini sil* seçeneğini **işaretlenmemiş** olarak bırakın.
2. Merhaba, [Azure portal](https://portal.azure.com), Git toohello **uzantıları** menüsüne VM hello ve hello kaldırma **VMSnapshot/VMSnapshotLinux** uzantısı.
3. Klasik mod tooResource Yöneticisi modundan Hello sanal makineyi geçirin. Depolama ve ağ toovirtual makine karşılık gelen ayrıca geçirilen tooResource Yöneticisi modunda olduğundan emin olun.
4. Bir kurtarma Hizmetleri kasası oluşturma ve yapılandırma hello üzerinde Yedekleme kullanarak sanal makine geçişi **yedekleme** kasa Panosu üzerinde eylem. Çok konusunda daha fazla bilgi edinin[kurtarma Hizmetleri kasasına yedeklemeyi etkinleştirme](backup-azure-vms-first-look-arm.md)
