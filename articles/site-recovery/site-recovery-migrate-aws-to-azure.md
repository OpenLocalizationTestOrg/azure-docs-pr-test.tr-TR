---
title: AWS tooAzure gelen aaaMigrate VM'ler | Microsoft Docs
description: "Çalışan nasıl toomigrate sanal makineleri bu makalede Azure Site RECOVERY'yi kullanarak Amazon Web Hizmetleri (AWS) tooAzure içinde."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Amazon Web Hizmetleri (AWS) tooAzure Azure Site Recovery ile sanal makineleri geçirme

Nasıl toomigrate AWS Windows hello tooAzure sanal makinelerle örnekleri bu makalede [Azure Site Recovery](site-recovery-overview.md) hizmet.

Geçiş, bir yük devretmeyi AWS tooAzure etkin değil. Yeniden çalışma makineler tooAWS olamaz ve devam eden çoğaltılmaz. Bu makalede hello Azure portalı içinde geçiş için hello adımları açıklar ve hello yönergeler için temel alan [bir fiziksel makine tooAzure çoğaltma](site-recovery-vmware-to-azure.md).

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Desteklenen işletim sistemleri

Site Recovery tüm işletim sistemleri aşağıdaki hello çalıştıran kullanılan toomigrate EC2 örnekleri olabilir:

- Windows (yalnızca 64 bit)
    - Windows Server 2008 R2 SP1 + (Citrix PV sürücüleri veya yalnızca AWS PV sürücüler. **RedHat PV sürücüleri çalışan örnekleri desteklenmez**) Windows Server 2012 Windows Server 2012 R2
- Linux (yalnızca 64 bit)
    - Red Hat Enterprise Linux 6.7 (yalnızca HVM sanallaştırılmış örnekleri)

## <a name="prerequisites"></a>Ön koşullar

İşte bu dağıtım için gerekenler:

* **Yapılandırma sunucusu**: Windows Server 2012 R2 çalıştıran bir Amazon EC2 VM hello yapılandırma sunucusu olarak dağıtılır. Merhaba yapılandırma sunucusu dağıtırken varsayılan olarak, hello diğer Azure Site Recovery bileşenleri (işlem sunucusu ve ana hedef sunucusu) yüklenir. Bu makalede hello Azure portalı içinde geçiş için hello adımları açıklar ve hello yönergeler için temel alan [daha fazla bilgi edinin](site-recovery-components.md)

* **EC2 örnekleri**: toomigrate istediğiniz Amazon EC2 sanal makineleri örnekleri hello.

## <a name="deployment-steps"></a>Dağıtım adımları

1. Kurtarma Hizmetleri kasası oluşturun.
2. Merhaba EC2 örneklerinizi güvenlik grubunun yapılandırılan kuralları tooallow iletişim toomigrate ve toodeploy hello yapılandırma sunucusu planlama hello örneği istediğiniz hello EC2 örneği arasında olması gerekir.

3. Merhaba üzerinde aynı Amazon sanal özel bulut olarak EC2 örneklerinizi ASR yapılandırma sunucusu dağıtın. Merhaba VMware başvurmak / fiziksel tooAzure önkoşulları yapılandırma sunucusu dağıtım gereksinimleri.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Yapılandırma sunucusu AWS içinde dağıtılır ve, Kurtarma Hizmetleri kasasına kayıtlı sonra hello yapılandırma sunucusu ve Site Recovery altyapısı bölümünde işlem sunucusunu aşağıda gösterildiği gibi görmeniz gerekir:

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Merhaba yapılandırma sunucusu dağıttıktan sonra (Bunun için too15 minustes sürebilir tooappear), onu hello VM'ler ile toomigrate istediğiniz iletişim kurabildiğini doğrulayın.

6. [Çoğaltma ayarlarını belirleme](site-recovery-setup-replication-settings-vmware.md).

7. Çoğaltmayı etkinleştirme: Merhaba toomigrate istediğiniz VM'ler için çoğaltma etkinleştirme. Merhaba EC2 Konsolu'ndan alabilirsiniz hello özel IP adresleri kullanan hello EC2 örneklerini bulabilir.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Merhaba EC2 örnekleri korumalı ve hello çoğaltma tooAzure tamamlandıktan sonra [bir yük devretme testi](site-recovery-test-failover-to-azure.md) toovalidate uygulamanızın performansını azure'da.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Bir yük devretme AWS tooAzure her VM için çalıştırın. İsteğe bağlı olarak, bir kurtarma planı oluşturun ve AWS tooAzure birden çok sanal makine bir yük devretme, toomigrate çalıştırın. [Daha fazla bilgi edinin](site-recovery-create-recovery-plans.md) kurtarma planları hakkında.

10. Geçiş için bir yük devretme toocommit gerek yoktur. Merhaba tam geçiş seçeneği bunun yerine, seçtiğiniz her makine için toomigrate istiyor. Geçişi tamamlamak eylemin Hello hello geçiş işlemini tamamlanır, hello makinesi için çoğaltma kaldırır ve Site Recovery hello makine için faturalama durdurur.

    ![Geçiş](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Sonraki adımlar

- [Geçirilen makinelerin tooenable çoğaltma hazırlama](site-recovery-azure-to-azure-after-migration.md) tooanother bölge olağanüstü durum kurtarma gerekir.
- [Azure sanal makinelerini çoğaltarak](site-recovery-azure-to-azure.md) iş yüklerinizi korumaya başlayın.
