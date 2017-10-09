---
title: "Azure VM'ler tooanother bölge çoğaltma Başlat aaaBefore | Microsoft Docs"
description: "Hello Azure Site Recovery hizmetini kullanarak Azure bölgeler arasında Azure Vm'lerini çoğaltma önce tootake gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>2. adım: Başlamadan önce

Merhaba gözden geçirdikten sonra [mimarisi](azure-to-azure-walkthrough-architecture.md) ile Azure bölgeler arasında Azure sanal makine (VM) çoğaltmak için [Azure Site Recovery](site-recovery-overview.md), bu makale tooverify Önkoşullar kullanın. 

- Merhaba makale bitirdikten sonra açık olmalıdır toomake hello dağıtım gerekli olan anlama çalışma ve hello önkoşul adımları tamamladınız.
- Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>
> Azure VM çoğaltma şu anda önizlemede değil.



## <a name="support-recommendations"></a>Destek önerileri

Gözden geçirme hello tabloda.

**Bileşen** | **Gereksinim**
--- | ---
**Kurtarma Hizmetleri kasası** | Merhaba hedefinde toouse olağanüstü durum kurtarma için istediğiniz Azure bölgesini kurtarma Hizmetleri kasası oluşturmanızı öneririz. Örneğin, Doğu ABD tooCentral ABD VM'ler kaynağında tooreplicate istiyorsanız hello kasa içinde Orta ABD oluşturun.
**Azure aboneliği** | Azure aboneliğiniz toouse hello olağanüstü durum kurtarma bölge olarak istediğiniz hello hedef konumda etkin toocreate VM'ler olmalıdır. Desteğe başvurun tooenable hello gerekli kotası.
**Hedef bölge kapasite** | Merhaba hedef Azure bölgesi, hello abonelik VM'ler, depolama hesapları ve ağ bileşenleri için yeterli kapasiteye sahip olmalıdır.
**Depolama** | Kullanım hello [depolama Kılavuzu](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) kaynağınız Azure VM'ler, tooavoid performans sorunları için.<br/><br/> Depolama hesapları hello olmalıdır hello kasasıyla aynı bölgede.<br/><br/> Orta ve Güney Hindistan toopremium hesapları çoğaltma yapamaz.<br/><br/> Çoğaltma hello varsayılan ayarlarla dağıtırsanız, Site Recovery gerekli hello depolama hesapları hello kaynak yapılandırmasını temel alarak oluşturur. Ayarları özelleştirirseniz hello izleyin [VM diskleri için ölçeklenebilirlik hedefleri](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Ağ** | Azure VM'ler, giden bağlantısını tooallow belirli URL'leri/IP aralıkları için gerekir.<br/><br/> Ağ hesapları hello olmalıdır hello kasasıyla aynı bölgede. 
**Azure VM** | Tüm hello son kök sertifikaların Windows/Linux Azure VM hello üzerinde olduğundan emin olun. Değilseniz, güvenlik kısıtlamaları nedeniyle mümkün tooregister hello Site kurtarma hizmetinde VM olmayacaktır.
**Azure kullanıcı hesabı** | Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) bir Azure sanal makinesinin tooenable çoğaltma.

Destek gereksinimlerinin tam listesi hello almak [destek matrisi](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Merhaba hesap izinleri ayarlama

1. Merhaba hakkında okuyun [izinleri](site-recovery-role-based-linked-access-control.md) çoğaltma için gerekir.
2. Aşağıdaki adımları [yönergeleri](../active-directory/role-based-access-control-configure.md#add-access) tooadd izinleri.


## <a name="verify-target-resources"></a>Hedef kaynakları doğrulayın

1. Azure aboneliği tooallow etkinleştirmek hello toocreate Vm'lerde hedef toouse toouse hello olağanüstü durum kurtarma bölge olarak istediğiniz olağanüstü durum kurtarma için bölgesini. Desteğe başvurun tooenable hello gerekli kotası.
2. Aboneliğinizi yeterli kaynakları tooenable VM'ler kaynağınız VM'ler eşleşen boyutlarına sahip olduğundan emin olun. Varsayılan olarak, çoğaltma, Site Recovery ayarlandığında Çekmeleri hello için aynı boyutta Merhaba, VM hedef veya en yakın olası boyutu hello. Daha fazla bilgi edinmek [sorun giderme](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) hedef kaynaklar.

## <a name="verify-azure-vm-certificates"></a>Azure VM sertifikaların doğrulama

1. Hello Windows veya Linux VM'ler tooreplicate istediğiniz tüm hello son kök sertifikaların mevcut olduğunu kontrol edin. Merhaba son kök sertifikaları mevcut değilse hello VM toosecurity kısıtlamaları nedeniyle kayıtlı tooSite kurtarma olamaz.
2. Windows VM'ler için aşağıdaki hello:

    - Böylece tüm hello güvenilen kök sertifikalar hello makinede hello VM tüm hello en son Windows güncelleştirmeleri yükleyin.
    - Bağlantısı kesilmiş bir ortamda hello standart Windows Update işlemi veya sertifikanın güncelleştirme işlemini kuruluş, tooget hello son kök sertifikaları ve hello vm'lerde güncelleştirilmiş bir CRL izleyin.
3. Linux VM'ler için Linux dağıtıcı tooget hello son güvenilen kök sertifikaları ve hello son sertifika iptal listesi hello VM üzerinde tarafından sağlanan hello yönergeleri izleyin. Daha fazla bilgi edinmek [sorun giderme](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) güvenilen kök sorunları.


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[3. adım: ağ planlama](azure-to-azure-walkthrough-network.md) tooset giden bağlantı kurma.
