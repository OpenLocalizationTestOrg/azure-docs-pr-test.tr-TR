---
title: "tooAzure çoğaltmak için Site Recovery destek matrisi aaaAzure | Microsoft Docs"
description: "Azure Site Recovery için hello desteklenen işletim sistemleri ve bileşenler özetler"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajanaki
ms.openlocfilehash: eae1db2ff1392d272f6b2eb0e3410da19d09da7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-tooazure"></a>Şirket içi tooAzure çoğaltmak için azure Site Recovery destek matrisi


Bu makalede, Azure Site çoğaltma ve kurtarma tooAzure kurtarma için desteklenen yapılandırmalar ve bileşenleri özetlenmektedir. Azure Site Recovery gereksinimleri hakkında daha fazla bilgi için bkz: Merhaba [Önkoşullar](site-recovery-prereq.md).


## <a name="support-for-deployment-options"></a>Dağıtım seçenekleri için destek

**Dağıtım** | **VMware/fiziksel sunucu** | **Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)** |
--- | --- | ---
**Azure portal** | Böylece, şirket içi VMware sanal makinelerini tooAzure depolama, Azure Resource Manager veya Klasik depolama ve ağlarla.<br/><br/> Yük devretme tooResource Manager tabanlı ya da Klasik VM'ler. | Böylece, şirket içi Hyper-V sanal makineleri tooAzure depolama Resource Manager veya Klasik depolama ve ağlar ile.<br/><br/> Yük devretme tooResource Manager tabanlı ya da Klasik VM'ler.
**Klasik portal** | Yalnızca Bakım modunda. Yeni kasa oluşturulamıyor. | Yalnızca Bakım modunda.
**PowerShell** | Şu anda desteklenmiyor. | Destekleniyor


## <a name="support-for-datacenter-management-servers"></a>Veri Merkezi Yönetimi sunucuları desteği

### <a name="virtualization-management-entities"></a>Sanallaştırma Yönetimi varlıklar

**Dağıtım** | **Destek**
--- | ---
**VMware sanal/fiziksel sunucu** | vCenter 6.5, 6.0 veya 5.5
**Hyper-V (Virtual Machine Manager ile)** | System Center Virtual Machine Manager 2016 ve System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > Windows Server 2016 ve 2012 R2 konakları bileşimi ile System Center Virtual Machine Manager 2016 bulut şu anda desteklenmiyor.

### <a name="host-servers"></a>Ana bilgisayar sunucuları

**Dağıtım** | **Destek**
--- | ---
**VMware sanal/fiziksel sunucu** | vSphere 6.5, 6.0, 5.5
**Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)** | Windows Server 2016, en son güncelleştirmeleri içeren Windows Server 2012 R2.<br></br>SCVMM kullandıysanız, Windows Server 2016 konakları SCVMM 2016 tarafından yönetilmelidir.


  >[!Note]
  >Windows Server 2016 ve 2012 R2 çalıştıran konaklar karıştırır bir Hyper-V sitesi şu anda desteklenmiyor. Kurtarma tooan alternatif konumu VM'ler için bir Windows Server 2016 konakta şu anda desteklenmiyor.

## <a name="support-for-replicated-machine-os-versions"></a>Çoğaltılan makinenin işletim sistemi sürümleri için destek

Korunan sanal makineler karşılamalıdır [Azure gereksinimleri](#failed-over-azure-vm-requirements) tooAzure çoğaltırken.
Aşağıdaki tablonun hello Azure Site Recovery kullanırken çeşitli dağıtım senaryolarında çoğaltılmış işletim sistemi desteği özetler. Bu destek, işletim sistemi Hello üzerinde çalışan herhangi bir iş yükünü belirtildiği için geçerlidir.

 **VMware/fiziksel sunucu** | **Hyper-V (ile/VMM olmadan)** |
--- | --- |
64-bit Windows Server 2012 R2, Windows Server 2012, Itanium tabanlı sistemler için Windows Server 2008 R2 ile en az SP1<br/>*Windows Server 2016* - VMware sanal makineleri ve fiziksel sunucuları üzerinde şu anda desteklenmiyor. <br/><br/> Red Hat Enterprise Linux: 5.2 too5.11, 6.1 too6.8, 7.0 too7.3 <br/><br/>Sent işletim sistemi: 5.2 too5.11, 6.1 too6.8, 7.0 too7.3 <br/><br/>Ubuntu 14.04 LTS server[ (çekirdek sürümleri desteklenir)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Ubuntu 16.04 LTS server[ (çekirdek sürümleri desteklenir)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Oracle Enterprise Linux 6.4, hello Red Hat uyumlu çekirdek veya kesilemeyen kurumsal çekirdek sürüm 3 (UEK3) çalıştıran 6.5 <br/><br/> SUSE Linux Enterprise Server 11 SP3 <br/><br/> SUSE Linux Enterprise Server 11 SP4 <br/>(Makineler SLES 11 SP3 tooSLES 11 SP4 çoğaltılan yükseltme desteklenmez. Çoğaltılmış bir makineden SLES 11SP3 tooSLES 11 SP4 ' yükseltildiyse, toodisable çoğaltma gerekir ve hello makine yeniden post hello yükseltme koruyun.) | Bir konuk işletim sistemi [Azure tarafından desteklenen](https://technet.microsoft.com/library/cc794868.aspx)


>[!IMPORTANT]
>(TooAzure kopyalayan geçerli tooVMware/fiziksel sunucular)
>
> Red Hat Enterprise Linux Server 7 + ve CentOS 7 + sunucularda, çekirdek sürüm 3.10.0-514 hello Azure Site Recovery Mobility hizmeti 9.8 sürümünden itibaren desteklenmektedir.<br/><br/>
> Merhaba 3.10.0-514 çekirdeğini hello Mobility hizmeti 9.8 sürümünden daha düşük bir sürümü ile gerekli toodisable çoğaltma, güncelleştirme hello hello Mobility hizmeti tooversion 9.8 sürümü'i ve çoğaltma yeniden etkinleştirme müşterilerdir.


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>VMware/fiziksel sunucular için desteklenen Ubuntu çekirdek sürümleri

**Sürüm** | **Mobility hizmeti sürümü** | **Çekirdek sürümü** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0-117-genel<br/>3.16.0-25-Generic too3.16.0-77-genel<br/>3.19.0-18-Generic too3.19.0-80-genel<br/>4.2.0-18-Generic too4.2.0-42-genel<br/>4.4.0-21-Generic too4.4.0 75-genel |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0-121-genel<br/>3.16.0-25-Generic too3.16.0-77-genel<br/>3.19.0-18-Generic too3.19.0-80-genel<br/>4.2.0-18-Generic too4.2.0-42-genel<br/>4.4.0-21-Generic too4.4.0 81 genel |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0-81-genel<br/>4.8.0-34-Generic too4.8.0-56-genel<br/>4.10.0-14-Generic too4.10.0 24-genel |


## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>Desteklenen dosya sistemleri ve Linux (VMware/fiziksel sunucuları) üzerinde Konuk depolama yapılandırmaları

Merhaba aşağıdaki dosya sistemleri ve depolama yapılandırması yazılım VMware veya fiziksel sunucuları üzerinde çalışan Linux sunucularda desteklenir:
* Dosya sistemleri: ext3, ext4, ReiserFS (Suse Linux Enterprise Server yalnızca), XFS
* Birim Yöneticisi: LVM2
* Çok yollu yazılım: cihaz Eşleyici

Paravirtualized depolama aygıtları (paravirtualized sürücüleri tarafından dışarı aktarılan) desteklenmez.<br/>
Birden çok sıra blok g/ç cihazları desteklenmez.<br/>
Merhaba HP CCISS depolama denetleyicisi ile fiziksel sunucuları desteklenmez.<br/>

>[!Note]
> Dizinleri aşağıdaki Linux sunucuları hello üzerinde (varsa ayrı bölümleri/dosya-sistemleri ayarlanmış) tüm hello üzerinde olmalıdır hello kaynak sunucudaki aynı diski (Merhaba işletim sistemi diski): / (kök), / Boot/usr, /usr/local, /var, / etc<br/><br/>
> Meta veri sağlama toplamı gibi XFS bağlanan dosya sistemlerinin XFSv5 özellikleri hello Mobility hizmeti 9.10 sürümünden başlayarak desteklenir. XFSv5 özellikleri kullanıyorsanız, Mobility hizmeti sürümü 9.10 veya sonraki sürümünü çalıştırdığınızdan emin olun. Merhaba xfs_info yardımcı programı toocheck hello XFS Süper blok kullanarak hello bölüm için kullanabilirsiniz. Ftype too1 ayarlarsanız XFSv5 özellikleri kullanılıyor.
>


## <a name="support-for-network-configuration"></a>Ağ yapılandırması için destek
Aşağıdaki tablolar hello ağ yapılandırma desteği, Azure Site Recovery tooreplicate tooAzure kullanan çeşitli dağıtım senaryolarında özetler.

### <a name="host-network-configuration"></a>Konak ağ yapılandırması

**Yapılandırma** | **VMware/fiziksel sunucu** | **Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)**
--- | --- | ---
NIC ekibi oluşturma | Evet<br/><br/>Fiziksel makineleri çoğaltıldığında desteklenmiyor| Evet
VLAN | Evet | Evet
IPv4 | Evet | Evet
IPv6 | Hayır | Hayır

### <a name="guest-vm-network-configuration"></a>Konuk VM ağ yapılandırması

**Yapılandırma** | **VMware/fiziksel sunucu** | **Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)**
--- | --- | ---
NIC ekibi oluşturma | Hayır | Hayır
IPv4 | Evet | Evet
IPv6 | Hayır | Hayır
Statik IP (Windows) | Evet | Evet
Statik IP (Linux) | Evet <br/><br/>Sanal makineler yeniden çalışma toouse DHCP yapılandırılmış olan  | Hayır
Multi-NIC | Evet | Evet

### <a name="failed-over-azure-vm-network-configuration"></a>Başarısız üzerinden Azure VM ağ yapılandırması

**Azure ağı** | **VMware/fiziksel sunucu** | **Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)**
--- | --- | ---
Express Route | Evet | Evet
ILB | Evet | Evet
ELB | Evet | Evet
Traffic Manager | Evet | Evet
Multi-NIC | Evet | Evet
Ayrılmış IP | Evet | Evet
IPv4 | Evet | Evet
Kaynak IP koru | Evet | Evet


## <a name="support-for-storage"></a>Depolama için destek
Aşağıdaki tablolar hello depolama yapılandırma desteği, Azure Site Recovery tooreplicate tooAzure kullanan çeşitli dağıtım senaryolarında özetler.

### <a name="host-storage-configuration"></a>Ana bilgisayar depolama yapılandırması

**Yapılandırma** | **VMware/fiziksel sunucu** | **Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)**
--- | --- | --- | ---
NFS | VMware için Evet<br/><br/> Fiziksel sunucuları için Hayır'ı | Yok
SMB 3.0 | Yok | Evet
SAN (İSCSI) | Evet | Evet
Çok yollu (MPIO)<br></br>İle test: Microsoft DSM, EMC PowerPath 5.7 SP4, EMC PowerPath DSM CLARiiON için | Evet | Evet

### <a name="guest-or-physical-server-storage-configuration"></a>Konuk veya fiziksel sunucu depolama yapılandırması

**Yapılandırma** | **VMware/fiziksel sunucu** | **Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)**
--- | --- | ---
VMDK | Evet | Yok
VHD/VHDX | Yok | Evet
Gen 2 VM | Yok | Evet
EFI/UEFI'YE| Hayır | Evet
Küme diskini paylaşılan | Hayır | Hayır
Şifrelenmiş disk | Hayır | Hayır
NFS | Hayır | Yok
SMB 3.0 | Hayır | Hayır
RDM | Evet<br/><br/> Fiziksel sunucuları için yok | Yok
Disk > 1 TB | Evet<br/><br/>Fazla 4095 GB | Evet<br/><br/>Fazla 4095 GB
Disk 4K kesim boyutu | Evet | Evet, nesil 1 VM'ler için desteklenen<br/><br/>Nesil 2 sanal makineleri için desteklenmez.
Şeritli disk > 1 TB birimle<br/><br/> LVM mantıksal birim yönetimi | Evet | Evet
Depolama alanları | Hayır | Evet
Sık kullanılan Ekle/Kaldır disk | Hayır | Hayır
Disk Dışla | Evet | Evet
Çok yollu (MPIO) | Yok | Evet

**Azure depolama alanı** | **VMware/fiziksel sunucu** | **Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)**
--- | --- | ---
LRS | Evet | Evet
GRS | Evet | Evet
RA-GRS | Evet | Evet
Seyrek erişimli depolama | Hayır | Hayır
Sık erişimli depolama| Hayır | Hayır
Rest(SSE) şifreleme| Evet | Evet
Premium depolama | Evet | Evet
İçeri/dışarı aktarma hizmeti | Hayır | Hayır


## <a name="support-for-azure-compute-configuration"></a>Azure işlem yapılandırma desteği

**Özellik işlem** | **VMware/fiziksel sunucu** | **Hyper-V (ile arama/olmadan Sanal Makine Yöneticisi)**
--- | --- | --- 
Kullanılabilirlik kümeleri | Evet | Evet
HUB | Evet | Evet  
Yönetilen diskler | Evet | Evet<br/><br/>Yeniden çalışma tooon içi Azure VM yönetilen disklerle şu anda desteklenmiyor.

## <a name="failed-over-azure-vm-requirements"></a>Başarısız üzerinden Azure VM gereksinimleri

Site Recovery tooreplicate sanal makineler ve Azure tarafından desteklenen herhangi bir işletim sistemini çalıştıran fiziksel sunucuları dağıtabilirsiniz. Buna çoğu Windows ve Linux sürümü dahildir. Böylece, şirket içi tooreplicate tooAzure çoğaltılırken Azure gereksinimleri aşağıdaki hello ile uymalıdır istediğiniz sanal makineleri.

**Varlık** | **Gereksinimleri** | **Ayrıntılar**
--- | --- | ---
**Konuk işletim sistemi** | Hyper-V tooAzure çoğaltma: Site Recovery tüm işletim sistemlerini destekler [Azure tarafından desteklenen](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> VMware ve fiziksel sunucu çoğaltma için: hello Windows ve Linux denetleyin [önkoşulları](site-recovery-vmware-to-azure-classic.md) | Önkoşul denetimi desteklenmeyen başarısız olur.
**Konuk işletim sistemi mimarisi** | 64 bit | Önkoşul denetimi desteklenmeyen başarısız olur
**İşletim sistemi disk boyutu** | GB'a too2048 çoğaltma yapıyorsanız **VMware Vm'lerini veya fiziksel sunucuları tooAzure**.<br/><br/>İçin fazla 2048 GB **Hyper-V nesil 1** VM'ler.<br/><br/>Fazla için 300 GB **Hyper-V 2. nesil sanal makineleri**.  | Önkoşul denetimi desteklenmeyen başarısız olur
**İşletim sistemi disk sayısı** | 1 | Önkoşul denetimi desteklenmeyen başarısız olur.
**Veri diski sayısı** | 64 veya daha az çoğaltma yapıyorsanız **VMware Vm'lerini tooAzure**; 16 veya daha az çoğaltma yapıyorsanız **Hyper-V sanal makineleri tooAzure** | Önkoşul denetimi desteklenmeyen başarısız olur
**Veri diski VHD boyutu** | Too4095 GB | Önkoşul denetimi desteklenmeyen başarısız olur
**Ağ bağdaştırıcıları** | Birden çok bağdaştırıcı desteklenir |
**Paylaşılan VHD** | Desteklenmiyor | Önkoşul denetimi desteklenmeyen başarısız olur
**FC disk** | Desteklenmiyor | Önkoşul denetimi desteklenmeyen başarısız olur
**Sabit disk biçimi** | VHD <br/><br/> VHDX | VHDX şu anda Azure'da desteklenmiyor olsa da, tooAzure başarısız olduğunda Site Recovery otomatik olarak VHDX tooVHD dönüştürür. Geri başarısız olduğunda tooon içi hello sanal makineler toouse hello VHDX biçimi devam eder.
**BitLocker'ı** | Desteklenmiyor | Bir sanal makine korumadan önce BitLocker'ı devre dışı bırakılmalıdır.
**VM adı** | 1 ile 63 karakter. Kısıtlı tooletters, rakam ve tire. Merhaba VM adı başlamalı ve bir harf veya sayı ile bitmelidir. | Site Recovery hello sanal makine özelliklerinde Hello değerini güncelleştirin.
**VM türü** | 1. nesil<br/><br/> Nesil 2--Windows | 2. nesil sanal makineleri (VHDX biçimlendirilmiş bir veya iki veri birimlerini içeren) temel bir işletim sistemi disk türüne sahip ve 300 GB disk alanı daha az desteklenir.<br></br>Linux nesil 2 sanal makineleri desteklenmez. [Daha fazla bilgi](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Kurtarma Hizmetleri kasası eylemler için destek

**Eylem** | **VMware/fiziksel sunucu** | **Hyper-V (Sanal Makine Yöneticisi)** | **Hyper-V (Virtual Machine Manager ile)**
--- | --- | --- | ---
Kasa kaynak grupları arasında taşıma<br/><br/> İçinde ve abonelikler arasında | Hayır | Hayır | Hayır
Depolama, ağ, Azure Vm'leri kaynak grupları arasında taşıma<br/><br/> İçinde ve abonelikler arasında | Hayır | Hayır | Hayır


## <a name="support-for-provider-and-agent"></a>Sağlayıcı ve aracı için destek

**Ad** | **Açıklama** | **En son sürümü** | **Ayrıntılar**
--- | --- | --- | --- | ---
**Azure Site Recovery sağlayıcısı** | Şirket içi sunucular ile Azure arasındaki iletişimi düzenler <br/><br/> Sanal Makine Yöneticisi sunucusu yoksa şirket içi Sanal Makine Yöneticisi sunucular veya Hyper-V sunucusunda yüklü | 5.1.19 ([portalından kullanılabilir](http://aka.ms/downloaddra)) | [En son özellikleri ve düzeltmeleri](https://support.microsoft.com/kb/3155002)
**Azure Site Recovery kurulumu (VMware tooAzure) birleşik** | Şirket içi VMware sunucular ile Azure arasındaki iletişimi düzenler <br/><br/> Şirket içi VMware sunucularda yüklü | 9.3.4246.1 (portalından kullanılabilir) | [En son özellikleri ve düzeltmeleri](https://support.microsoft.com/kb/3155002)
**Mobility hizmeti** | Şirket içi VMware sunucularını/fiziksel sunucular ile Azure/ikincil site arasında çoğaltma koordinatları<br/><br/> VMware VM veya fiziksel sunucularda yüklü tooreplicate istiyor  | Yok (portalından kullanılabilir) | Yok
**Microsoft Azure kurtarma Hizmetleri (MARS) aracısı** | Hyper-V sanal makineleri ve Azure arasında çoğaltma koordinatları<br/><br/> Şirket içi Hyper-V sunucuları (ile veya bir Sanal Makine Yöneticisi sunucusu olmadan) yüklü | En son Aracı ([portalından kullanılabilir](http://aka.ms/latestmarsagent)) |






## <a name="next-steps"></a>Sonraki adımlar
[Önkoşulları denetleme](site-recovery-prereq.md)
