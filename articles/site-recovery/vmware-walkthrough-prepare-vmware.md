---
title: "aaaPrepare şirket içi VMware kaynaklar için Azure Site Recovery ile çoğaltma tooAzure | Microsoft Docs"
description: "VMware Vm'leri tooAzure depolama üzerinde çalışan iş yüklerini çoğaltmak için gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>6. adım: şirket içi VMware çoğaltma tooAzure hazırlama

Bu makale tooprepare şirket içi VMware sunucularını toointeract Azure Site Recovery ile Merhaba yönergeleri kullanın ve VMWare Vm'lerini hello mobilite hizmetinin yüklenmesi için hazırlayın. Merhaba Mobility Hizmeti Aracısı tooreplicate tooAzure istediğiniz tüm şirket içi sanal makinelerin yüklenmelidir.

## <a name="prepare-for-automatic-discovery"></a>Otomatik bulma işlemi için hazırlama

Site Recovery vSphere ESXi konakları (ile veya bir vCenter sunucusu olmadan) üzerinde çalışan sanal makineleri otomatik olarak bulur. Otomatik bulma, Site kurtarma gereksinimlerini bir hesap tooaccess ana bilgisayarlar ve sunucular için:

1. toouse adanmış bir hesap oluşturma bir rolde (Merhaba aşağıdaki tabloda açıklanan hello izinlerle hello vCenter düzeyi. Gibi bir ad verin **Azure_Site_Recovery**.
2. Ardından, hello vSphere ana bilgisayar/vCenter sunucusu üzerinde bir kullanıcı oluşturun ve hello rol toohello kullanıcı atayın. Site Recovery dağıtımı sırasında bu kullanıcı hesabı belirtin.


### <a name="vmware-account-permissions"></a>VMware hesabı izinleri

Site kurtarma erişim tooVMware hello işlem sunucusu tooautomatically bulmak için sanal makineleri ve yük devretme ve sanal makineleri geri dönmesi gerekir.

- **Geçiş**: herhangi bir zamanda bunları geri başarısız olmadan toomigrate VMware Vm'lerini tooAzure'ni yalnızca isterseniz, salt okunur rolüyle VMware hesabı kullanabilirsiniz. Bu tür bir rol, yük devretme çalıştırabilirsiniz ancak korumalı kaynak makineleri kapatmayı olamaz. Bu geçiş için gerekli değildir.
- **Replicate/Recover**: toodeploy (çoğaltılır, yük devretme, yeniden çalışma) tam çoğaltma hello hesabı oluşturma ve diskleri kaldırma gibi işlemleri yapabilir toorun olmalıdır isterseniz, üzerinde sanal makineleri vb. destekleyen.
- **Otomatik bulma**: en az bir salt okunur hesabı gereklidir.


**Görev** | **Gerekli hesap/rol** | **İzinler** | **Ayrıntılar**
--- | --- | --- | ---
**İşlem sunucusu VMware sanal makineleri otomatik olarak bulur.** | En az bir salt okunur kullanıcının gerekiyor | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol = salt okunur | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** nesnesi, toohello alt nesneler (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).
**Yük devretme** | En az bir salt okunur kullanıcının gerekiyor | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol = salt okunur | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** toohello alt nesneleri (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).<br/><br/> Geçiş amacıyla, ancak değil tam çoğaltma, yük devretme, yeniden çalışma için kullanışlıdır.
**Yük devretme ve yeniden çalışma** | Merhaba gerekli izinlere sahip bir rol (Azure_Site_Recovery) oluşturun ve hello rol tooa VMware kullanıcı veya grup atayın öneririz | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol Azure_Site_Recovery =<br/><br/> Veri deposu alanı Ayır ->, veri deposu, alt düzey dosya işlemleri göz atın, dosyayı kaldırmak, sanal makine dosyalarını güncelleştir<br/><br/> Ağ -> Ağ atama<br/><br/> Kaynak VM atamak tooresource havuzu ->, VM güç beslemeli geçirmek, VM güç beslemeli geçirme<br/><br/> Görevler oluşturma görevi, güncelleştirme görevi -><br/><br/> Sanal Makine Yapılandırma -><br/><br/> Sanal makine -> etkileşimde bulunma yanıt soru, cihaz bağlantısı ->, CD ortamı yapılandırmak, disket ortamı, kapatma, açma, VMware araçları yükleme yapılandırın<br/><br/> Sanal makine -> Stok Oluştur ->, kaydetme, kaydı<br/><br/> Sanal makine sağlama -> izin sanal makine indirme ->, sanal makine dosyalarını karşıya yükleme izin ver<br/><br/> Sanal makine anlık görüntüleri -> Kaldır anlık görüntüleri -> | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** nesnesi, toohello alt nesneler (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>Merhaba mobilite hizmetinin göndermeli yüklemesi için hazırlama

Merhaba mobilite hizmetinin yüklenmesi tooreplicate istediğiniz tüm sanal makineler. Merhaba Site kurtarma işlemi sunucusundan gönderme yüklemesi ve yükleme yöntemleri gibi System Center Configuration Manager kullanarak el ile yükleme de dahil olmak üzere, yolları tooinstall hello hizmet mevcuttur.

Toouse anında yükleme istiyorsanız tooprepare Site Recovery tooaccess hello VM kullanabileceğiniz bir hesap gerekir.

- Bir etki alanı veya yerel hesabı kullanın
- Windows, bir etki alanı hesabı kullanmıyorsanız toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir. Bu, hello kaydetmek altında toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, hello DWORD girdisi eklemek **LocalAccountTokenFilterPolicy**, 1 değerine sahip.
- CLI Windows'dan tooadd hello kayıt defteri girdisini isterseniz, yazın:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- Linux için kök hello kaynak Linux sunucuda hello hesabı olmalıdır.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 7: bir kasa oluşturun](vmware-walkthrough-create-vault.md)
