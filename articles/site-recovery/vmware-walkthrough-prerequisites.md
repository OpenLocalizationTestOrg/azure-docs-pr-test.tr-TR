---
title: "Azure Site RECOVERY'yi kullanarak VMware tooAzure çoğaltma için aaaPrerequisites | Microsoft Docs"
description: "Hello Azure Site Recovery hizmetini kullanarak VMware sanal makinelerini tooAzure üzerinde çalışan iş yüklerini çoğaltılması hello önkoşullar özetlenmektedir."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 14f8e9713b42a1d8da71223fbbb7a6b7c4303adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-vmware-tooazure-replication"></a>2. adım: VMware tooAzure çoğaltma hello önkoşullarını gözden geçirme

Aşağıdaki tablonun hello özetlenen hello önkoşulları okuyun.

**Önkoşul** | **Ayrıntılar**
--- | ---
**Azure** | Hakkında bilgi edinin [Azure gereksinimleri](site-recovery-prereq.md#azure-requirements)
**Şirket içi yapılandırma sunucusu** | Windows Server 2012 R2 çalıştıran bir VMware VM gerekir ya da daha sonra. Site Recovery dağıtımı sırasında bu sunucusu ayarlayın.<br/><br/> Varsayılan hello işlem tarafından sunucu ve ana hedef sunucusu Ayrıca bu VM yüklenir. Ölçeği artırma, ayrı bir işlem sunucusu gerekebilir ve hello sahip olduğunda hello yapılandırma sunucusuyla aynı gereksinimleri.<br/><br/> Bu bileşenler hakkında daha fazla bilgi [burada](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Şirket içi VMware sunucuları** | 6.5, 6.0, 5.5, 5.1 ile en son güncelleştirmeleri çalıştıran bir veya daha fazla VMware vSphere sunucuları. Sunucular, aynı ağ hello yapılandırma sunucusu (veya ayrı işlem sunucusu) hello alanında bulunmalıdır.<br/><br/> VCenter server 6.5, 6.0 veya 5.5 hello en son güncelleştirmeleri ile çalışan toomanage konakları öneririz.
**Şirket içi sanal makineleri** | Tooreplicate çalışıyor istediğiniz sanal makineleri bir [işletim sistemi desteklenen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)ve uygun olması [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). VM VMware araçları çalışıyor olması gerekir.
**URL'leri** | Merhaba yapılandırma sunucusu toothese URL'leri erişmesi gereken:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.<br/></br> Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.<br/></br> IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.<br/><br/> Merhaba MySQL yüklemek için bu URL'ye izin ver: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility hizmeti** | Her çoğaltılmış VM'de yüklü.




## <a name="limitations"></a>Sınırlamalar

Dağıtmadan önce hello tabloda özetlenen hello kısıtlamaları anladığınızdan emin olun.

**Sınırlama** | **Ayrıntılar**
--- | ---
**Azure** | Depolama ve ağ hesapları hello olmalıdır hello kasasıyla aynı bölgede<br/><br/> Premium depolama hesabı kullanırsanız, standart bir etmeniz hesap toostore çoğaltma günlüklerini depolamak<br/><br/> Orta ve Güney Hindistan toopremium hesapları çoğaltma yapamaz.
**Şirket içi yapılandırma sunucusu** | VMware VM bağdaştırıcı türü VMXNET3 olmalıdır. Öyle değilse, [bu güncelleştirmeyi yükleyin](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> vSphere Powerclı 6.0 yüklenmesi gerekir.<br/><br> Merhaba makine bir etki alanı denetleyicisi olmaması gerekir. Merhaba makine statik bir IP adresi olmalıdır.<br/><br/> Merhaba ana bilgisayar adı 15 karakter uzunluğunda olmalıdır veya daha az ve işletim sistemi İngilizce olmalıdır.
**VMware** | Site Recovery yeni vCenter desteklemez ve vSphere 6.5 ve 6.0 özellikleri gibi vCenter VMotion'ı, sanal birimler ve depolama DRS arası.
**VM’ler** | Doğrulama [Azure VM sınırlamaları](site-recovery-prereq.md#azure-requirements)<br/><br/> Şifrelenmiş disklerle VM'ler veya UEFI/EFI Önyükleme olan VM'ler çoğaltma yapamaz.<br/><br> Paylaşılan disk kümelerini desteklenmez. NIC ekibi oluşturma Hello kaynak VM varsa, dönüştürülür tooa tek NIC yük devretme sonrasında.<br/><br/> Sanal makineleri bir iSCSI diski varsa, Site Recovery bu tooa VHD dosyasını yük devretme sonrasında dönüştürür. Merhaba iSCSI hedef hello Azure VM tarafından ulaşılabiliyorsa tooit bağlanır ve onu ve hello VHD görür. Bu durumda, hello iSCSI hedef bağlantısını kesin.<br/><br/> Aynı iş yükünü toobe kurtarılan hello çalıştıran VM'ler sağlayan tooenable çoklu VM tutarlılığını istiyorsanız birlikte tooa tutarlı veri noktası, bağlantı noktası 20004 hello VM açın.<br/><br/> Windows hello C sürücüsünde yüklenmesi gerekir. Merhaba işletim sistemi diski, temel ve dinamik olmayan olması gerekir. Merhaba veri diski dinamik olabilir.<br/><br/> Linux/Etc/Hosts dosyaları vm'lerde tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin giriş içermelidir. Merhaba ana bilgisayar adı, bağlama noktaları, aygıt adı, sistem yolu ve dosya adları (/ etc; / usr) İngilizce yalnızca olmalıdır.<br/><br/> Belirli türlerdeki [Linux depolama](site-recovery-support-matrix-to-azure.md#support-for-storage) desteklenir.<br/><br/>Oluşturma veya ayarlama **disk.enableUUID=true** hello VM Ayarları'nda. Bu tutarlı bir UUID toohello VMDK, sunar, böylece doğru bağlar ve yalnızca delta değişiklikler tam çoğaltma olmadan yeniden çalışma sırasında aktarılan geri tooon içi olmasını sağlar.


## <a name="next-steps"></a>Sonraki adımlar

- Tam dağıtımını yaptığınız, çok gidin[3. adım: kapasite planlama](vmware-walkthrough-capacity.md)
- Basit test dağıtımını yaptığınız, çok gidin[4. adım: ağ planlama](vmware-walkthrough-network.md).
