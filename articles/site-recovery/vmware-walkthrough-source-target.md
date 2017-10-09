---
title: "Merhaba kaynak ve hedef Azure Site Recovery ile VMware çoğaltma tooAzure için aaaSet | Microsoft Docs"
description: "Azure Site Recovery ile VMware Vm'lerini tooAzure depolama çoğaltma için kaynak ve hedef ayarlarını Hello adımları tooset özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>8. adım: hello kaynak ve hedef VMware çoğaltma tooAzure için ayarlama

Bu makalede nasıl çoğaltırken tooconfigure kaynak ve hedef ayarları şirket içi VMware sanal makineleri tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Merhaba yapılandırma sunucusunu ayarlamayı, hello kasaya kaydetmek ve Vm'leri bulma.

1. Tıklatın **Site kurtarma** > **1. adım: altyapıyı hazırlama** > **kaynak**.
2. Yapılandırma sunucusu yoksa, tıklatın **+ yapılandırma sunucusu**.
3. İçinde **Sunucu Ekle**, denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.
4. Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.
5. Merhaba kasa kayıt anahtarını indirin. Birleşik Kurulum'u çalıştırdığınızda bu gerekir. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

   ![Kaynağı ayarlama](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Merhaba kasasına Hello yapılandırma sunucusuna kaydedin

, Önce hello aşağıdaki başlayın, ardından birleşik Kurulum tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda çalıştırın.
    - Hızlı bir video özeti

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Merhaba yapılandırma sunucusunda VM, o hello sistem saati ile eşitlenir emin olun bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Eşleşmelidir. Önde 15 dakika ise veya arkasında kurulum başarısız olabilir.
    - Kurulum bir yerel yönetici hello yapılandırma sunucusundaki VM olarak çalıştırın.
    - TLS 1.0 hello VM etkin olduğundan emin olun.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Merhaba yapılandırma sunucusu da yüklenebilir [hello komut satırından](http://aka.ms/installconfigsrv).



## <a name="connect-toovmware-servers"></a>TooVMware sunucularına bağlanmak

tooallow Azure Site Recovery toodiscover şirket içi ortamınızda çalışan sanal makineler, VMware vCenter sunucusu veya Site Recovery ile vSphere ESXi konakları tooconnect gerekir. Başlamadan önce hello aşağıdakilere dikkat edin:

- Merhaba sunucuda hello vCenter sunucusu veya yönetici ayrıcalıkları olmayan bir hesapla vSphere ana tooSite kurtarma eklerseniz, hello hesabının etkin Bu ayrıcalıkları gerekir:
    - Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine, vSphere dağıtılmış anahtar.
    - Merhaba vCenter sunucusu depolama görünümleri izinleri olması gerekir.
- VMware sunucularını tooSite kurtarma eklediğinizde, 15 dakika alabilir veya onlar için daha uzun tooappear hello Portalı'nda.

### <a name="add-hello-account-for-automatic-discovery"></a>Otomatik bulma için Hello hesabı ekleyin

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>Bağlantı kurma

Tooservers şu şekilde bağlanın:

1. Seçin **+ vCenter** toostart bir VMware vCenter sunucusu veya bir VMware vSphere ESXi konağı bağlanma.
2. İçinde **vCenter ekleme**hello vSphere ana bilgisayar veya vCenter sunucusu için bir kolay ad belirtin ve sonra başlangıç IP adresi veya hello sunucusunun FQDN'sini belirtin.
3. VMware sunucularınızı farklı bir bağlantı noktası isteklerini yapılandırılmış toolisten olmadıkça hello bağlantı noktası 443'tür bırakın. Tooconnect toohello VMware vCenter veya vSphere ESXi sunucu hello hesabı seçin. **Tamam** düğmesine tıklayın.
4. Site Recovery bağlayan tooVMware sunucuları hello kullanarak belirtilen ayarlarını ve sanal makineleri bulur.

> [!NOTE]
> Bir sunucu veya ana bilgisayar hello vCenter veya ana bilgisayar sunucusunda yönetici ayrıcalıklarına sahip olmayan bir hesapla ekliyorsanız hello hesabı etkin Bu ayrıcalıkları olduğundan emin olun: Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine ve vSphere dağıtılmış anahtar. Ayrıca, hello VMware vCenter server hello depolama ayrıcalık etkinleştirilmiş görünümlere gerekir.


## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama

Merhaba hedef ortamını ayarlama önce bir Azure depolama hesabı ve sanal ağ kurulumu olduğundan emin olun.

1. Tıklatın **altyapıyı hazırlama** > **hedef**, ve hello toouse istediğiniz Azure aboneliğini seçin.
2. Belirtin, hedef dağıtım modeli Resource Manager tabanlı veya Klasik olup.
3. Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.

   ![Hedef](./media/vmware-walkthrough-source-target/gs-target.png)
4. Bir depolama hesabı veya ağı oluşturmadıysanız, tıklatın **+ depolama hesabı** veya **+ ağ**, toocreate bir Resource Manager hesabı ya da ağ satır içi.

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 9: bir çoğaltma ilkesini ayarlayın](vmware-walkthrough-replication.md)
