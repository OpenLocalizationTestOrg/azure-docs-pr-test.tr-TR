---
title: " Azure Site Recovery VMware vCenter Server'da yönetme | Microsoft Docs"
description: "Bu makalede nasıl ekleyin ve Azure Site Recovery VMware Vcenter'da yönetin."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>VMware vCenter Server Azure Site kurtarma yönetme
Bu makalede hello ele bir VMware vCenter üzerinde gerçekleştirilen çeşitli Site kurtarma işlemleri.

## <a name="prerequisites"></a>Ön koşullar

**VMware vCenter ve VMware vSphere ESX konak desteği** | **Ayrıntılar** |
|--- | --- |
|**Şirket içi VMware sunucuları** | 6.0, 5.5, 5.1 ile en son güncelleştirmeleri çalıştıran bir veya daha fazla VMware vSphere sunucuları. Sunucular, aynı ağ hello yapılandırma sunucusu (veya ayrı işlem sunucusu) hello alanında bulunmalıdır.<br/><br/> Bir vCenter 6.0 veya 5.5 hello son güncelleştirmeleriyle çalıştıran sunucu toomanage ana öneririz. Sürüm 6.0 dağıttığınızda 5.5 içinde kullanılabilir olan özellikler desteklenir.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Otomatik bulma için bir hesap hazırlama
Site kurtarma hello işlem sunucusu tooautomatically bulmak için sanal makineler ve yük devretme ve sanal makinelerin yeniden çalışma için erişim tooVMware gerekir.

* **Geçiş**: herhangi bir zamanda bunları geri başarısız olmadan toomigrate VMware sanal makineleri tooAzure'ni yalnızca isterseniz, salt okunur rolüyle VMware hesabı kullanabilirsiniz. Bu tür bir rol, yük devretme çalıştırabilirsiniz ancak korumalı kaynak makineleri kapatmayı olamaz. Bu geçiş için gerekli değildir.
* **Replicate/Recover**: toodeploy (çoğaltılır, yük devretme, yeniden çalışma) tam çoğaltma hello hesabı oluşturma ve diskleri kaldırma gibi işlemleri yapabilir toorun olmalıdır istiyorsanız, sanal makineyi destekleyen.
* **Otomatik bulma**: en az bir salt okunur hesabı gereklidir.


|**Görevler** | **Gerekli hesap/rol** | **İzinler** | **Ayrıntılar**|
|--- | --- | --- | ---|
|**İşlem sunucusu VMware sanal makineleri otomatik olarak bulur.** | En az bir salt okunur kullanıcının gerekiyor | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol = salt okunur | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** nesnesi, toohello alt nesneler (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).|
|**Yük devretme** | En az bir salt okunur kullanıcının gerekiyor | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol = salt okunur | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** toohello alt nesneleri (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).<br/><br/> Geçiş amacıyla, ancak değil tam çoğaltma, yük devretme, yeniden çalışma için kullanışlıdır.|
|**Yük devretme ve yeniden çalışma** | Merhaba gerekli izinlere sahip bir rol (AzureSiteRecoveryRole) oluşturun ve hello rol tooa VMware kullanıcı veya grup atayın öneririz | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol AzureSiteRecoveryRole =<br/><br/> Veri deposu alanı Ayır ->, veri deposu, alt düzey dosya işlemleri göz atın, dosyayı kaldırmak, sanal makine dosyalarını güncelleştir<br/><br/> Ağ -> Ağ atama<br/><br/> Kaynak VM atamak tooresource havuzu ->, VM güç beslemeli geçirmek, VM güç beslemeli geçirme<br/><br/> Görevler oluşturma görevi, güncelleştirme görevi -><br/><br/> Sanal Makine Yapılandırma -><br/><br/> Sanal makine -> etkileşimde bulunma yanıt soru, cihaz bağlantısı ->, CD ortamı yapılandırmak, disket ortamı, kapatma, açma, VMware araçları yükleme yapılandırın<br/><br/> Sanal makine -> Stok Oluştur ->, kaydetme, kaydı<br/><br/> Sanal makine sağlama -> izin sanal makine indirme ->, sanal makine dosyalarını karşıya yükleme izin ver<br/><br/> Sanal makine anlık görüntüleri -> Kaldır anlık görüntüleri -> | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** nesnesi, toohello alt nesneler (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Bir hesap tooconnect tooVMware vCenter Server oluşturun / VMware vSphere EXSi konağı
1. Merhaba kısayolunu kullanarak hello yapılandırma sunucusu ve başlatma hello cspsconfigtool.exe oturum hello Masaüstü üzerinde yerleştirilir.
2. Tıklatın **hesabı Ekle** hello üzerinde **hesabı Yönet** sekmesi.

  ![Hesabı Ekle](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Hello hesap ayrıntılarını girin ve Tamam tooadd hello hesabı'nı tıklatın. Merhaba hesap hello listelenen hello ayrıcalıklarına sahip olmalıdır [otomatik bulma için bir hesap hazırlama](#prepare-an-account-for-automatic-discovery) bölümü.

  >[!NOTE]
  Yukarı hello Site Recovery hizmeti ile eşitlenmiş hello hesap bilgileri toobe yaklaşık 15 dakika sürer.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>İlişkilendirme bir VMware vCenter / ESX VMware vSphere ana bilgisayar (Ekle vCenter)
* Üzerinde Azure portal Merhaba, çok Gözat*YourRecoveryServicesVault* > **Site Recovery altyapısı** > **Configuration Server'lar**  >  *ConfigurationServer*
* Merhaba yapılandırma sunucunun ayrıntılarına Merhaba + vCenter'ı tıklatın düğmesi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Kullanılan kimlik bilgileri tooconnect toohello vCenter sunucusunu değiştirmek / vSphere ESXi ana bilgisayar

1. Merhaba yapılandırma sunucusu ve başlatma hello cspsconfigtool.exe oturum aç
2. Tıklatın **hesabı Ekle** hello üzerinde **hesabı Yönet** sekmesi.

  ![Hesabı Ekle](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Merhaba yeni hesap ayrıntılarını girin ve Tamam tooadd hello hesabı'nı tıklatın. Merhaba hesap hello listelenen hello ayrıcalıklarına sahip olmalıdır [otomatik bulma için bir hesap hazırlama](#prepare-an-account-for-automatic-discovery) bölümü.
4. Üzerinde Azure portal Merhaba, çok Gözat*YourRecoveryServicesVault* > **Site Recovery altyapısı** > **Configuration Server'lar**  >  *ConfigurationServer*
5. Merhaba yapılandırma sunucunun Ayrıntıları sayfasında hello tıklatın **sunucusunu Yenile eylemi** düğmesi.
6. Merhaba yenileme sunucu işi tamamlandıktan sonra hello vCenter Server tooopen hello vCenter Özet sayfasını seçin.
7. Select hello hello yeni hesap eklenen **vCenter sunucusu/vSphere ana bilgisayar hesabı** alanına gelin ve hello **kaydetmek** düğmesi.

  ![değiştirme hesabı](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Azure Site Recovery Vcenter'da Sil
1. Üzerinde Azure portal Merhaba, çok Gözat*YourRecoveryServicesVault* > **Site Recovery altyapısı** > **Configuration Server'lar**  >  *ConfigurationServer*
2. Merhaba yapılandırma sunucunun ayrıntılarına hello vCenter Server tooopen hello vCenter Özet sayfasını seçin.
3. Tıklatın hello üzerinde **silmek** düğmesini toodelete hello vCenter

  ![hesabı Sil](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Toodelete hello vCenter Server gerekir ve tekrar tekrar ekleyin ardından toomodify hello Vcenter IP adresi/FQDN, bağlantı noktası ayrıntıları gerekiyorsa.
