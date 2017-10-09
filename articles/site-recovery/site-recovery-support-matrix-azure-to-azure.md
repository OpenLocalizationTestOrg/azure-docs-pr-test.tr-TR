---
title: "aaaAzure Site Recovery destek matrisi ' Azure tooAzure çoğaltılması | Microsoft Docs"
description: "Olağanüstü Durum Kurtarma (DR) gereksinimleriniz için tek bir bölge tooanother gelen hello desteklenen işletim sistemleri ve Azure sanal makineleri (VM'ler) Azure Site Recovery çoğaltma için yapılandırmaları özetler."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>Azure tooAzure çoğaltmak için azure Site Recovery destek matrisi


>[!NOTE]
>
> Azure sanal makineler için Site Recovery çoğaltma şu anda önizlemede değil.

Bu makalede, Azure Site Recovery çoğaltma ve tek bir bölge tooanother bölgesinden Azure sanal makinelerini kurtarma için desteklenen yapılandırmalar ve bileşenleri özetlenmektedir.

## <a name="user-interface-options"></a>Kullanıcı arabirimi seçenekleri

**Kullanıcı arabirimi** |  **Desteklenen / desteklenmeyen**
--- | ---
**Azure portal** | Destekleniyor
**Klasik portal** | Desteklenmiyor
**PowerShell** | Şu anda desteklenmiyor
**REST API** | Şu anda desteklenmiyor
**CLI** | Şu anda desteklenmiyor


## <a name="resource-move-support"></a>Kaynak taşıma desteği

**Kaynak taşıma türü** | **Desteklenen / desteklenmeyen** | **Açıklamalar**  
--- | --- | ---
**Kasa kaynak grupları arasında taşıma** | Desteklenmiyor |Kaynak grupları arasında hello kurtarma Hizmetleri kasası taşınamıyor.
**İşlem, depolama ve ağ kaynak grupları arasında taşıma** | Desteklenmiyor |Çoğaltma etkinleştirdikten sonra bir sanal makine (veya ilişkili bileşenlerini depolama ve ağ gibi) taşırsanız toodisable çoğaltma gerekir ve hello sanal makinesi için çoğaltma yeniden etkinleştirin.


## <a name="support-for-deployment-models"></a>Dağıtım modelleri için destek

**Dağıtım modeli** | **Desteklenen / desteklenmeyen** | **Açıklamalar**  
--- | --- | ---
**Klasik** | Destekleniyor | Yalnızca klasik bir sanal makine çoğaltabilir ve klasik sanal makine olarak kurtarın. Resource Manager sanal makine olarak kurtaramazsınız. Klasik bir VM sanal ağ ve doğrudan tooan Azure bölgesi olmadan dağıtırsanız, desteklenmiyor.
**Resource Manager** | Destekleniyor |

## <a name="support-for-replicated-machine-os-versions"></a>Çoğaltılan makinenin işletim sistemi sürümleri için destek

Destek aşağıda hello Hello üzerinde çalışan herhangi bir iş yükünü belirtilen işletim sistemi için geçerlidir.

#### <a name="windows"></a>Windows

- Windows Server 2016 (Sunucu Çekirdeği ve masaüstü deneyimi olan sunucu) *
- Windows Server 2012 R2
- Windows Server 2012
- Itanium tabanlı sistemler için Windows Server 2008 R2 ile en az SP1

>[!NOTE]
>
> \*Windows Server 2016 Nano Server desteklenmiyor.

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7, 6,8, 7.0, 7.1, 7.2, 7.3
- CentOS 6.5, 6.6 6.7, 6,8, 7.0, 7.1, 7.2, 7.3
- Ubuntu 14.04 LTS Server [ (çekirdek sürümleri desteklenir)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Ubuntu 16.04 LTS Server [ (çekirdek sürümleri desteklenir)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Enterprise Linux 6.4, hello Red Hat uyumlu çekirdek veya kesilemeyen kurumsal çekirdek sürüm 3 (UEK3) çalıştıran 6.5
- SUSE Linux Enterprise Server 11 SP3

>[!NOTE]
>
> Ubuntu sunucuları parola kullanarak kimlik doğrulaması ve oturum açma, ve hello bulut init paket tooconfigure bulut sanal makineleri kullanarak, parolayı (bağlı olarak hello cloudinit yapılandırmasını.) yük devretme sırasında devre dışı oturum açma dayalı sahip Parola tabanlı oturum açma hello Azure portalında sanal makinede yük devredildi hello (altında Merhaba destek + sorun giderme bölümüne) hello ayarları menüsünden hello parolasını sıfırlayarak hello sanal makinede yeniden etkinleştirilebilir.

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Azure sanal makineler için desteklenen Ubuntu çekirdek sürümleri

**Sürüm** | **Mobility hizmeti sürümü** | **Çekirdek sürümü** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0-117-genel<br/>3.16.0-25-Generic too3.16.0-77-genel<br/>3.19.0-18-Generic too3.19.0-80-genel<br/>4.2.0-18-Generic too4.2.0-42-genel<br/>4.4.0-21-Generic too4.4.0 75-genel |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0-121-genel<br/>3.16.0-25-Generic too3.16.0-77-genel<br/>3.19.0-18-Generic too3.19.0-80-genel<br/>4.2.0-18-Generic too4.2.0-42-genel<br/>4.4.0-21-Generic too4.4.0 81 genel |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0-81-genel<br/>4.8.0-34-Generic too4.8.0-56-genel<br/>4.10.0-14-Generic too4.10.0 24-genel |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Desteklenen dosya sistemleri ve Linux işletim sistemi çalıştıran Azure sanal makinelerinde Konuk depolama yapılandırmaları

* Dosya sistemleri: ext3, ext4, ReiserFS (Suse Linux Enterprise Server yalnızca), XFS
* Birim Yöneticisi: LVM2
* Çok yollu yazılım: cihaz Eşleyici

## <a name="region-support"></a>Bölge desteği

Çoğaltabilir ve hello içinde iki tüm bölgeler arasında sanal makineleri kurtarma aynı coğrafi küme.

**Coğrafi küme** | **Azure bölgeleri**
-- | --
Amerika | Doğu Kanada, Kanada Merkezi, Güney Orta ABD, Batı Orta ABD, Doğu ABD, Doğu ABD 2, Batı ABD, Batı ABD 2, Orta ABD, Kuzey Orta ABD
Avrupa | Birleşik Krallık Batı, Birleşik Krallık Güney, Kuzey Avrupa, Batı Avrupa
Asya | Güney Hindistan, Orta Hindistan, Güneydoğu Asya, Doğu Asya, Japonya Doğu, Kore Orta, Kore Güney Batı, Japonya
Avustralya   | Avustralya Doğu, Avustralya Güneydoğu

>[!NOTE]
>
> Brezilya Güney bölge için yalnızca çoğaltabilir ve yük devretme tooone Orta Güney ABD, Batı Orta ABD, Doğu ABD, Doğu ABD 2, Batı ABD, Batı ABD 2 ve Kuzey Orta ABD bölgeler ve başarısız, geri.


## <a name="support-for-compute-configuration"></a>İşlem yapılandırması için destek

**Yapılandırma** | **Desteklenen/desteklenmeyen** | **Açıklamalar**
--- | --- | ---
Boyut | Tüm Azure VM boyutu en az 2 CPU çekirdekleri ve 1 GB RAM | Çok başvuran[Azure sanal makine boyutları](../virtual-machines/windows/sizes.md)
Kullanılabilirlik kümeleri | Destekleniyor | Portalı'nda 'çoğaltmasını Etkinleştir' adımı sırasında hello varsayılan seçeneği kullanırsanız, hello kullanılabilirlik otomatik olarak Kaynak bölgesi yapılandırmasına göre oluşturulan kümesidir. Merhaba hedef kullanılabilirlik kümesinde değiştirebileceğiniz ' yinelenmiş öğesi > Ayarlar > işlem ve ağ > kullanılabilirlik kümesi ' dilediğiniz zaman.
Karma kullanımı Avantajı (HUB) VM'ler | Destekleniyor | Ayrıca Hello kaynak VM etkin HUB lisansı varsa, hello Test yük devretme veya yük devretme VM hello HUB lisans kullanır.
Sanal makine ölçek kümeleri | Desteklenmiyor |
Microsoft Azure galeri görüntüleri - yayımlandı | Destekleniyor | Site Recovery tarafından desteklenen bir işletim sisteminde Hello VM çalıştığı sürece desteklenen
-Üçüncü taraf yayımlanan Azure galeri görüntüleri | Destekleniyor | Site Recovery tarafından desteklenen bir işletim sisteminde Hello VM çalıştığı sürece desteklenir.
Özel görüntü - üçüncü taraf yayımlanan | Destekleniyor | Site Recovery tarafından desteklenen bir işletim sisteminde Hello VM çalıştığı sürece desteklenir.
Site Recovery kullanarak sanal makineleri geçişi | Destekleniyor | Bu doğruysa bir VMware/fiziksel makineye geçirilen Site RECOVERY'yi kullanarak tooAzure, toouninstall hello mobility hizmeti'nın daha eski bir sürümü gerekiyor ve tooanother Azure bölgesi çoğaltma önce hello makineyi yeniden başlatın.

## <a name="support-for-storage-configuration"></a>Depolama yapılandırması için destek

**Yapılandırma** | **Desteklenen/desteklenmeyen** | **Açıklamalar**
--- | --- | ---
En yüksek işletim sistemi disk boyutu | 1023 GB | Çok başvuran[VM'ler tarafından kullanılan diskler.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
En fazla veri diski boyutu | 1023 GB | Çok başvuran[VM'ler tarafından kullanılan diskler.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Veri diski sayısı | Fazla belirli bir Azure VM boyutu tarafından desteklenen gibi 64 | Çok başvuran[Azure sanal makine boyutları](../virtual-machines/windows/sizes.md)
Geçici disk | Her zaman Çoğaltmada hariç | Geçici disk her zaman çoğaltmadan dışlandı. Herhangi bir kalıcı veri Azure Kılavuzu göredir geçici diskteki moduna geçirmelisiniz değil. Çok başvuran[Azure vm'lerinde geçici disk](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk) daha fazla ayrıntı için.
Oranı hello diskteki verileri değiştirme | En fazla disk başına 6 MB/sn | Merhaba ortalama veri üzerinde oranı değiştirirseniz hello disk 6 MBps sürekli olarak, çoğaltma yakalamaz. Ancak, bazen veri veri bloğu ise ve hello veri değişikliği hızı süre için 6 MBps büyük olduğundan ve gelir, çoğaltma Yakala. Bu durumda, biraz Gecikmeli kurtarma noktalarını görebilirsiniz.
Standart depolama hesapları disklerde | Destekleniyor |
Premium depolama hesapları disklerde | Destekleniyor | Bir VM premium ve standart depolama hesapları üzerinden yayılan diskler varsa, sahip olduğunuz farklı bir hedef depolama hesabı her disk tooensure için seçebileceğiniz hello hedef bölgede aynı depolama yapılandırması
Standart yönetilen disk | Desteklenmiyor |  
Premium yönetilen diskleri | Desteklenmiyor |
Depolama alanları | Destekleniyor |         
Bekleyen (SSE) şifreleme | Destekleniyor | Önbellek ve hedef depolama hesapları için etkin SSE depolama hesabı seçebilirsiniz.     
Azure Disk şifrelemesi (ADE) | Desteklenmiyor |
Sık kullanılan Ekle/Kaldır disk | Desteklenmiyor | Veri diski hello VM üzerinde ekleyip, toodisable çoğaltma gerekir ve çoğaltma hello VM için yeniden etkinleştirin.
Disk Dışla | Desteklenmiyor|   Geçici disk varsayılan olarak çıkarılır.
LRS | Destekleniyor |
GRS | Destekleniyor |
RA-GRS | Destekleniyor |
ZRS | Desteklenmiyor |  
Seyrek erişimli ve sık erişimli depolama | Desteklenmiyor | Sanal makine disklerini seyrek erişimli ve sık erişimli depolama üzerinde desteklenmez.

>[!IMPORTANT]
> Merhaba uyduğundan emin [depolama Kılavuzu](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) performans sorunları tooavoid kaynağınız Azure sanal makineleri için. Merhaba varsayılan ayarları izlerseniz, Site Recovery hello kaynak yapılandırmasını temel alarak gerekli hello depolama hesapları oluşturun. Özelleştirme ve kendi ayarlarınızı seçerseniz, hello izlediğinizden emin olun (.. / storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) kaynağınız VM'ler.

## <a name="support-for-network-configuration"></a>Ağ yapılandırması için destek
**Yapılandırma** | **Desteklenen/desteklenmeyen** | **Açıklamalar**
--- | --- | ---
Ağ arabirimi (NIC) | Belirli bir Azure VM boyutu tarafından desteklenen NIC'ler fazla sayısı | Test yük devretme veya yük devretme işlemi kapsamında Hello VM oluşturulduğunda NIC'ler oluşturulur. Merhaba sayısına NIC'ler hello yük devretme VM VM çoğaltma etkinleştirme hello aynı anda sahip NIC hello kaynak hello sayısına bağlıdır. Ekleyin veya NIC çoğaltma etkinleştirdikten sonra Kaldır, hello yük devretme VM NIC sayısına etkilemez.
İnternet Yük Dengeleyici | Destekleniyor | Tooassociate ihtiyacınız hello önceden yapılandırılmış bir azure Otomasyonu komut dosyası kullanarak bir kurtarma planında yük dengeleyici.
İç yük dengeleyici | Destekleniyor | Tooassociate ihtiyacınız hello önceden yapılandırılmış bir azure Otomasyonu komut dosyası kullanarak bir kurtarma planında yük dengeleyici.
Genel IP| Destekleniyor | Bir tane oluşturun ve toohello bir kurtarma planı bir azure Otomasyonu komut dosyası kullanarak NIC ilişkilendirmek tooassociate zaten mevcut olan genel IP toohello NIC gerekir.
NSG üzerinde NIC'ye (Resource Manager)| Destekleniyor | Tooassociate hello NSG toohello bir kurtarma planı bir azure Otomasyonu komut dosyası kullanarak NIC gerekir.  
NSG alt (Resource Manager ve klasik)| Destekleniyor | Tooassociate hello NSG toohello bir kurtarma planı bir azure Otomasyonu komut dosyası kullanarak NIC gerekir.
NSG VM'ye (Klasik)| Destekleniyor | Tooassociate hello NSG toohello bir kurtarma planı bir azure Otomasyonu komut dosyası kullanarak NIC gerekir.
Ayrılmış IP (statik IP) / kaynak IP koru | Destekleniyor | Merhaba NIC hello kaynak VM üzerinde bir statik IP yapılandırması ve hello hedef alt varsa aynı IP toohello yük devretme VM atanan kullanılabilir hello sahiptir. Merhaba hedef alt aynı IP kullanılabilir, biri de kullanılabilir IP'leri hello hello yoksa hello alt bu VM için ayrılmıştır. Tercih ettiğiniz bir sabit IP belirtebilirsiniz ' yinelenmiş öğesi > Ayarlar > işlem ve ağ > ağ arabirimleri. Merhaba NIC seçin ve hello alt ağı ve tercih ettiğiniz IP belirtin.
Dinamik IP| Destekleniyor | Hello NIC hello kaynak VM üzerinde dinamik IP yapılandırmasına sahip olsa hello hello yük devretme NIC'nin VM de varsayılan olarak dinamik bir işlemdir. Tercih ettiğiniz bir sabit IP belirtebilirsiniz ' yinelenmiş öğesi > Ayarlar > işlem ve ağ > ağ arabirimleri. Merhaba NIC seçin ve hello alt ağı ve tercih ettiğiniz IP belirtin.
Traffic Manager tümleştirmesi | Destekleniyor | Önceden, trafik Yöneticisi hello trafiği yönlendirilmiş toohello uç noktadaki bir düzenli aralıklarla ve toohello yük devretme durumunda hedef bölgede kaynak bölgede olduğunu şekilde yapılandırabilirsiniz.
Azure DNS yönetilen | Destekleniyor |
Özel DNS  | Destekleniyor |    
Kimliği doğrulanmamış Proxy | Destekleniyor | Çok başvuran[Ağ Kılavuzu belge.](site-recovery-azure-to-azure-networking-guidance.md)    
Doğrulanmış bir Proxy | Desteklenmiyor | Merhaba VM için giden bağlantı doğrulanmış bir proxy kullanıyorsa, Azure Site RECOVERY'yi kullanarak yinelenemez.  
Şirket içi (ile veya ExpressRoute olmadan) site tooSite VPN| Destekleniyor | Merhaba Udr'ler ve Nsg'ler hello Site kurtarma trafiği yönlendirilmiş tooon içi değil bir şekilde yapılandırıldığından emin olun. Çok başvuran[Ağ Kılavuzu belge.](site-recovery-azure-to-azure-networking-guidance.md)  
VNET tooVNET bağlantı | Destekleniyor | Çok başvuran[Ağ Kılavuzu belge.](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>Sonraki adımlar
- Daha fazla bilgi edinmek [Azure Vm'lerini çoğaltma kılavuz ağ oluşturma](site-recovery-azure-to-azure-networking-guidance.md)
- İş yükleri tarafından korumaya başlamak [Azure Vm'lerini çoğaltma](site-recovery-azure-to-azure.md)
