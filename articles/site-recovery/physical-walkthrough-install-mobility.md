---
title: "aaaInstall hello fiziksel sunucu tooAzure çoğaltma için Mobility hizmetini | Microsoft Docs"
description: "Bu makalede nasıl tooinstall hello Mobility Hizmeti Aracısı tooAzure hello Azure Site Recovery hizmeti ile çoğaltma fiziksel sunucularda açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>9. adım: hello Mobility hizmetini yükleme


Bu makalede nasıl çoğaltırken tooinstall hello Mobility hizmeti bileşeninin Windows/Linux fiziksel sunucuları tooAzure hello kullanarak, şirket içi [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

Merhaba Mobility hizmeti bir makinede veri Yazar yakalar ve bunları toohello işlem sunucusuna iletir. Tooreplicate tooAzure istediğiniz her sunucuda yüklenmelidir.

Merhaba Mobility hizmeti el ile yükleyebilirsiniz veya hello anında yüklemesinden kullanarak Site Recovery işlem çoğaltma etkinleştirildiğinde, sunucu veya System Center Configuration Manager gibi bir araç kullanarak. Anında yükleme kullanırsanız, çoğaltmayı etkinleştirme hello hizmet hello sunucusuna yüklenir.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>El ile yükleme

1. Merhaba denetleyin [Önkoşullar](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) el ile yükleme.
2. İzleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) hello portal'ı kullanarak el ile yükleme.
3. Merhaba komut satırından tooinstall tercih ederseniz, izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Merhaba işlem sunucusundan yükle

Bir makine için çoğaltma etkinleştirdiğinizde toopush hello Mobility hizmeti yüklemesi hello işlem sunucusundan istiyorsanız, hello işlem sunucusu tooaccess hello makine tarafından kullanılan bir hesabınızın olması gerekir. Merhaba hesabı yalnızca hello gönderme yüklemesi için kullanılır.

1. Bir hesabı oluşturmadıysanız, bu yönergeleri kullanarak bunu yapın:

    - Bir etki alanı veya yerel hesabı kullanın
    - Windows, bir etki alanı hesabı kullanmıyorsanız toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir. Bu, hello kaydetmek altında toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, hello DWORD girdisi eklemek **LocalAccountTokenFilterPolicy**, 1 değerine sahip.
    - CLI Windows'dan tooadd hello kayıt defteri girdisini isterseniz, yazın:

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Linux için kök hello kaynak Linux sunucuda hello hesabı olmalıdır.

2. Ardından izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) toopush hello Mobility hizmeti Windows veya Linux çalıştıran sanal makineleri üzerinde istiyorsanız.

## <a name="other-installation-methods"></a>Diğer yükleme yöntemleri

- [Hakkında bilgi edinin](site-recovery-install-mobility-service-using-sccm.md) hello Mobility hizmetinin Yapılandırma Yöneticisi'ni kullanarak yükleme
- [Hakkında bilgi edinin](site-recovery-automate-mobility-service-install.md) Azure Otomasyonu DSC'ye yükleme.


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 10: çoğaltmasını etkinleştir](physical-walkthrough-enable-replication.md)
