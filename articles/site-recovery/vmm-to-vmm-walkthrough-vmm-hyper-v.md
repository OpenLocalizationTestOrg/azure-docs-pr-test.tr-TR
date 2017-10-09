---
title: "VMM ve Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site için aaaSet | Microsoft Docs"
description: "Açıklar nasıl tooset System Center VMM sunucuları ve Hyper-V ana bilgisayarları için çoğaltma tooa ikincil VMM sitesi."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>4. adım: VMM ve Hyper-V VM çoğaltma tooa ikincil site için Hyper-V ayarlama 

System Center Virtual Machine Manager (VMM) sunucuları ve Hyper-V sanal makine (VM) çoğaltma tooa ikincil site için Hyper-V konakları için ağ hazırladığınız sonra ayarlama kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure Portalı'nda. 

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="prepare-vmm-servers"></a>VMM sunucuları hazırlama 

tooprepare dağıtımı için:


1. VMM sunucuları hello ile uyumlu olduğundan emin olun [destek gereksinimlerini](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), ve [dağıtımının önkoşulları](vmm-to-vmm-walkthrough-prerequisites.md).
2. VMM sunucusu bağlı toohello olduğundan emin olun Internet ve erişim toothese URL'lere sahip.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.
    - Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.
    - IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.
3. Merhaba VMM sunucusu olduğundan emin olun [ağ eşlemesi için hazır](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Hyper-V konakları/kümeleri hazırlama

1. Hyper-V konakları/kümeleri hello ile uyumlu olduğundan emin olun [destek gereksinimlerini](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), ve [dağıtımının önkoşulları](vmm-to-vmm-walkthrough-prerequisites.md).
2. Hello gereksinimleri için doğrulama [Hyper-V sanal makineleri](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. Doğrulama [ağ](site-recovery-support-matrix-to-sec-site.md#network-configuration) ve [depolama](site-recovery-support-matrix-to-sec-site.md#storage) gereksinimleri.
4. Hyper-V konakları bağlı toohello olduğundan emin olun Internet ve erişim toothese URL'lere sahip.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.
    - Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.
    - IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.

## <a name="prepare-for-single-server-deployment"></a>Tek sunucu dağıtımı için hazırlama


Yalnızca tek bir VMM sunucusu varsa, sanal makineleri hello VMM bulut Hyper-V konakları olarak çok çoğaltabilirsiniz[Azure](hyper-v-site-walkthrough-overview.md) veya tooa ikincil VMM bulut, bu belgede açıklandığı gibi. Bulutlar arasında çoğaltma sorunsuz olmadığından hello ilk seçenek öneririz.

Bulutlar arasında tooreplicate istiyorsanız, tek tek başına VMM sunucusuyla veya esnetilen Windows kümesinde dağıtılan tek bir VMM sunucusuyla çoğaltabilirsiniz

### <a name="replicate-with-a-standalone-vmm-server"></a>Bir tek başına VMM sunucusuyla Çoğalt

Bu senaryoda, sanal makine hello birincil site olarak hello tek VMM sunucusu dağıtın ve Site kurtarma ve Hyper-V çoğaltma kullanarak bu VM tooa ikincil bir sitenin çoğaltma.

1. **Bir Hyper-V VM'de VMM ayarlama**. Merhaba SQL Server örneği üzerinde hello VMM tarafından kullanılan birlikte bulundurma önerdiğimiz aynı VM. Yalnızca bir VM oluşturulan toobe bulunduğundan bu zamandan tasarruf sağlar. VMM kurtarabilmek toouse uzak SQL Server örneğini istediğiniz ve bir kesinti oluşursa, bu örnek toorecover gerekir.
2. **Merhaba VMM sunucusunda yapılandırılmış en az iki bulut bulunduğundan emin olun**. Bir bulut tooreplicate istediğiniz ve diğer bulut hello VM'ler hello ikincil konumu olarak kullanılacak hello içerir. Merhaba istediğiniz tooprotect ile uyumlu olması gerekir hello VM'ler içeren bulut [Önkoşullar](#prerequisites).
3. Site Recovery, bu makalede açıklanan şekilde ayarlayın. Oluşturma ve hello VMM sunucusu bir kasaya kaydetmek bir çoğaltma ilkesini ayarlayın ve çoğaltmayı etkinleştirin. Merhaba kaynak ve hedef VMM adları olması hello aynı. Merhaba ağ üzerinden ilk çoğaltmanın gerçekleşir belirtin.
4. Ağ eşlemesi ayarlamanız hello VM ağı hello ikincil bulut için hello birincil bulut toohello VM ağı için eşleyin.
5. Merhaba Hyper-V Yöneticisi konsolunda, Hyper-V çoğaltma hello VMM VM içeren hello Hyper-V ana bilgisayarda ve hello VM çoğaltmayı etkinleştirebilirsiniz. Site Recovery, Hyper-V çoğaltma ayarlarını Site Recovery tarafından geçersiz kılınmış olmayan tooensure tarafından korunan hello VMM sanal makine tooclouds eklemeyin emin olun.
6. Kullandığınız yük devretme için kurtarma planları oluşturursanız, kaynak için aynı VMM sunucusu hello ve hedefleyebilirsiniz.
7. Tam bir kesinti yük devri ve aşağıdaki şekilde kurtarın:

   1. Planlanmamış bir yük devretme hello Hyper-V Yöneticisi konsolunda hello ikincil site, toofail hello birincil VMM VM toohello ikincil sitesi üzerinde çalıştırın.
   2. VMM VM çalışır durumda o hello doğrulayın ve çalıştırılması, hello kasadaki planlanmamış yük devretme toofail hello VM'ler üzerinde birincil toosecondary bulutlardan çalıştırın ve. Merhaba yük devretme kaydetmek ve gerekirse alternatif bir kurtarma noktası seçin.
   3. Tüm kaynaklar Hello planlanmamış yük devretme işlemi tamamlandıktan sonra hello birincil siteden yeniden erişilebilir.
   4. Merhaba birincil site yeniden hello Hyper-V Manager konsolunda hello ikincil sitedeki kullanılabilir olduğunda, çoğaltmayı tersine çevirme hello VMM VM için etkinleştirin. Bu, ikincil tooprimary hello VM için çoğaltma başlatır.
   5. Planlanmış bir yük devretme hello Hyper-V Yöneticisi konsolunda hello ikincil site, toofail hello VMM VM toohello birincil site üzerinden çalıştırın. Merhaba yük devretme uygulayın. Böylece Hello VMM VM yeniden birincil toosecondary çoğaltma çoğaltmayı tersine çevirme etkinleştirin.
   6. Merhaba kurtarma Hizmetleri kasasına hello iş yükü sanal makinelerinize, ikincil tooprimary çoğaltma toostart ters çoğaltmayı etkinleştirin.
   7. Bir planlı yük devretme toofail geri hello iş yükü VM'ler toohello birincil site çalıştırmak hello kurtarma Hizmetleri kasasına. Merhaba yük devretme toocomplete tamamlama. Daha sonra çoğaltmayı tersine çevirme toostart çoğaltma hello yükünden VM'ler birincil toosecondary etkinleştirin.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>Esnetilen VMM kümesi ile çoğaltma

Tek başına VMM sunucusu tooa ikincil site çoğaltılan VM olarak dağıtmak yerine, VMM yüksek oranda kullanılabilir bir VM Windows Yük devretme kümesinde olarak dağıtarak yapabilirsiniz. Bu, iş yükü esnekliği ve donanım hatalarına karşı koruma sağlar. Site Recovery hello VMM VM ile toodeploy coğrafi olarak ayrı siteler arasında uzatma bir kümede dağıtılması gerekir. toodo bu:

1. Windows Yük devretme kümesindeki bir sanal makinede VMM yükleme ve başlangıç seçeneği toorun hello server kurulumu sırasında yüksek oranda kullanılabilir olarak seçin.
2. Merhaba ikincil sitedeki hello veritabanının çoğaltmasını olmasını sağlamak VMM tarafından kullanılan hello SQL Server örneği SQL Server AlwaysOn Kullanılabilirlik grupları ile çoğaltılması.
3. Bu makale toocreate bir kasa Hello yönergeleri izleyin, hello sunucuyu kaydetmek ve koruma ayarlama. Her VMM sunucusunda hello küme kurtarma Hizmetleri kasası hello tooregister gerekir. toodo Bu, etkin bir düğümde hello sağlayıcı yükleyin ve hello VMM sunucusunu kaydedin. Ardından hello sağlayıcısı diğer düğümlere yükleyin.
4. Kesinti oluştuğunda hello VMM sunucusu karşılık gelen SQL Server veritabanını devredilir ve hello ikincil siteden erişilebilir.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[5. adım: bir kasasını oluşturup](vmm-to-vmm-walkthrough-create-vault.md).
