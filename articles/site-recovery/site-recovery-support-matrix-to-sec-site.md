---
title: "Azure Site Recovery ile çoğaltma tooa ikincil site için aaaSupport Matrisi | Microsoft Docs"
description: "Azure Site Recovery için hello desteklenen işletim sistemleri ve bileşenler özetler"
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
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 0b2bbc86aff52308d5a90a56d7a3ff4286877740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="support-matrix-for-replication-tooa-secondary-site-with-azure-site-recovery"></a>Azure Site Recovery ile çoğaltma tooa ikincil site için destek matrisi

Bu makalede, Azure Site Recovery tooreplicate tooa ikincil şirket içi site kullandığınızda nelerin desteklendiği özetlenmektedir.

## <a name="deployment-options"></a>Dağıtım seçenekleri

**Dağıtım** | **VMware/fiziksel sunucu** | **Hyper-V (ile/SCVMM olmadan)**
--- | --- | --- | ---
**Azure portal** | Şirket içi VMware sanal makinelerini toosecondary VMware sitesi.<br/><br/> Merhaba karşıdan [Inmage Scout Kullanıcı Kılavuzu](http://download.microsoft.com/download/E/0/8/E08B3BCE-3631-4CED-8E65-E3E7D252D06D/InMage_Scout_Standard_User_Guide_8.0.1.pdf) (hello Azure portal'ın kullanılamaz). | Böylece, şirket içi VMM Bulutları tooa ikincil VMM bulutundaki Hyper-V Vm'lerini.<br></br> VMM desteklenmiyor  <br/><br/> Yalnızca standart Hyper-V çoğaltma için. SAN desteklenmiyor.
**Klasik portal** | Yalnızca Bakım modunda. Yeni kasa oluşturulamıyor. | Yalnızca Bakım modu<br></br> SCVMM desteklenmiyor
**PowerShell** | Desteklenmiyor | Destekleniyor<br></br> SCVMM desteklenmiyor

## <a name="on-premises-servers"></a>Şirket içi sunucular

### <a name="virtualization-servers"></a>Sanallaştırma sunucuları

**Dağıtım** | **Destek**
--- | ---
**VMware sanal/fiziksel sunucu** | vSphere 6.0, 5.5 veya 5.1 en son güncelleştirme
**Hyper-V (VMM ile)** | VMM 2016 ve VMM 2012 R2

  >[!Note]
  > Windows Server 2016 ve 2012 R2 ana bilgisayarları karışımına sahip VMM 2016 Bulutlar şu anda desteklenmiyor.

### <a name="host-servers"></a>Ana bilgisayar sunucuları

**Dağıtım** | **Destek**
--- | ---
**VMware sanal/fiziksel sunucu** | vCenter 5.5 veya 6.0 (yalnızca 5.5 özellikleri için destek)
**Hyper-V (VMM yok)** | İkincil site tooa çoğaltılması bir desteklenen yapılandırma
**VMM ile Hyper-V** | Merhaba en son güncelleştirmeleri içeren Windows Server 2012 R2 ve Windows Server 2016.<br/><br/> Windows Server 2016 konaklar VMM 2016 tarafından yönetilmelidir.

## <a name="support-for-replicated-machine-os-versions"></a>Çoğaltılan makinenin işletim sistemi sürümleri için destek
Aşağıdaki tablonun hello Azure Site Recovery kullanırken karşılaşılan çeşitli dağıtım senaryolarında işletim sistemi desteği özetler. Bu destek, işletim sistemi Hello üzerinde çalışan herhangi bir iş yükünü belirtildiği için geçerlidir.

**VMware/fiziksel sunucu** | **Hyper-V (VMM ile)**
--- | --- | ---
64-bit Windows Server 2012 R2, Windows Server 2012, Itanium tabanlı sistemler için Windows Server 2008 R2 ile en az SP1<br/><br/> Red Hat Enterprise Linux 6.7, 7.1, 7.2 <br/><br/> Centos 6.5, 6.6 6.7, 7.0, 7.1, 7.2 <br/><br/> Oracle Enterprise Linux 6.4 veya hello Red Hat uyumlu çekirdek veya kesilemeyen kurumsal çekirdek sürüm 3 (UEK3) çalıştıran 6.5 <br/><br/> SUSE Linux Enterprise Server 11 SP3 | Herhangi bir işletim sistemi Konuk [Hyper-V tarafından desteklenen](https://technet.microsoft.com/library/mt126277.aspx)

>[!Note]
>Depolama aşağıdaki hello ile yalnızca Linux makineler çoğaltılabilir: dosya sistemi (EXT3, ETX4, ReiserFS, XFS); Çok yollu yazılım aygıtı Eşleyici; Birim Yöneticisi (LVM2).
>HP CCISS denetleyicisi depolama ile fiziksel sunucuları desteklenmez.
>Merhaba ReiserFS dosya sistemi yalnızca SUSE Linux Enterprise Server 11 SP3 üzerinde desteklenir.

## <a name="network-configuration"></a>Ağ yapılandırması

### <a name="hosts"></a>Ana bilgisayarlar

**Yapılandırma** | **VMware/fiziksel sunucu** | **Hyper-V (VMM ile)**
--- | --- | ---
NIC ekibi oluşturma | Evet | Evet
VLAN | Evet | Evet
IPv4 | Evet | Evet
IPv6 | Hayır | Hayır

### <a name="guest-vms"></a>Konuk sanal makineleri

**Yapılandırma** | **VMware/fiziksel sunucu** | **Hyper-V (VMM ile)**
--- | --- | ---
NIC ekibi oluşturma | Hayır | Hayır
IPv4 | Evet | Evet
IPv6 | Hayır | Hayır
Statik IP (Windows) | Evet | Evet
Statik IP (Linux) | Evet | Evet
Multi-NIC | Evet | Evet


## <a name="storage"></a>Depolama

### <a name="host-storage"></a>Ana bilgisayar depolama

**Depolama (ana bilgisayar)** | **VMware/fiziksel sunucu** | **Hyper-V (VMM ile)**
--- | --- | ---
NFS | Evet | Yok
SMB 3.0 | Yok | Evet
SAN (İSCSI) | Evet | Evet
Çok yollu (MPIO) | Evet | Evet

### <a name="guest-or-physical-server-storage"></a>Konuk veya fiziksel sunucu depolama

**Yapılandırma** | **VMware/fiziksel sunucu** | **Hyper-V (VMM ile)**
--- | --- | ---
VMDK | Evet | Yok
VHD/VHDX | Yok | Evet (too16 diskleri)
Gen 2 VM | Yok | Evet
Küme diskini paylaşılan | Evet  | Hayır
Şifrelenmiş disk | Hayır | Hayır
UEFI| Hayır | Yok
NFS | Hayır | Hayır
SMB 3.0 | Hayır | Hayır
RDM | Evet | Yok
Disk > 1 TB | Hayır | Evet
Şeritli disk > 1 TB birimle<br/><br/> LVM | Evet | Evet
Depolama alanları | Hayır | Evet
Sık kullanılan Ekle/Kaldır disk | Hayır | Hayır
Disk Dışla | Hayır | Evet
Çok yollu (MPIO) | Yok | Evet

## <a name="vaults"></a>kasaları

**Eylem** | **VMware/fiziksel sunucu** | **Hyper-V (VMM ile)**
--- | --- | ---
Kaynak grupları (içinde veya abonelikler arasında) arasında taşıma kasaları | Hayır | Hayır
Depolama, ağ, Azure Vm'leri kaynak grupları (içinde veya abonelikler arasında) arasında taşıma | Hayır | Hayır

## <a name="provider-and-agent"></a>Sağlayıcı ve aracı

**Ad** | **Açıklama** | **En son sürümü** | **Ayrıntılar**
--- | --- | --- | --- | ---
**Azure Site Recovery sağlayıcısı** | Şirket içi sunucular ile Azure arasındaki iletişimi düzenler <br/><br/> VMM sunucusu yoksa şirket içi VMM sunucularında veya Hyper-V sunucularında yüklü | 5.1.19 ([portalından kullanılabilir](http://aka.ms/downloaddra)) | [En son özellikleri ve düzeltmeleri](https://support.microsoft.com/kb/3155002)
**Mobility hizmeti** | Şirket içi VMware sunucuları veya fiziksel sunucular ve hello ikincil site arasında çoğaltma koordinatları<br/><br/> VMware VM veya tooreplicate istediğiniz fiziksel sunucularda yüklü  | Yok (portalından kullanılabilir) | Yok


## <a name="next-steps"></a>Sonraki adımlar

- [VMM Bulutları tooa ikincil sitedeki Hyper-V Vm'lerini çoğaltma](site-recovery-vmm-to-vmm.md)
- [VMware Vm'lerini ve fiziksel sunucuları tooa ikincil siteye çoğaltma](site-recovery-vmware-to-vmware.md)
