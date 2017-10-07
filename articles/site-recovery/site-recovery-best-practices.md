---
title: aaaAzure Site Recovery en iyi uygulamalar | Microsoft Docs
description: "Bu makalede Azure Site Recovery dağıtımı için en iyi uygulamalar açıklanmaktadır"
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Hazır toodeploy Azure Site Recovery Al

Bu makalede nasıl tooprepare Azure Site Recovery dağıtımı için.

## <a name="protecting-hyper-v-virtual-machines"></a>Hyper-V sanal makinelerini koruma

Hyper-V sanal makinelerini korumaya yönelik birkaç dağıtım seçeneğiniz vardır. Şirket içi Hyper-VMs tooAzure veya tooa ikincil veri merkezine çoğaltabilirsiniz. Her dağıtım için farklı gereksinimler vardır.

**Gereksinim** | **(VMM ile) tooAzure Çoğalt** | **Çoğaltma Hyper-V sanal makineleri tooAzure (VMM yok)** | **Hyper-V Vm'lerini (VMM ile) toosecondary site Çoğalt** | **Ayrıntılar**
---|---|---|---|---
**VMM** | System Center 2012 R2 üzerinde çalışan VMM <br/><br/>Bir veya daha fazla VMM ana bilgisayar grubu içeren en az bir VMM bulutu. | NA | VMM sunucusu üzerinde en az çalışan hello birincil ve ikincil sitelerde en son güncelleştirmeleri içeren System Center 2012 SP1. <br/><br/> Her VMM sunucusunda en az bir bulut. Bulutlar hello Hyper-V Kapasite profili kümesine sahip olması.<br/><br/> Merhaba kaynak bulut en az bir VMM konak grubu olması gerekir. | İsteğe bağlı. System Center VMM sipariş tooreplicate Hyper-V sanal makineleri tooAzure dağıtılan toohave gerekmez, ancak bunu yaparsanız toomake hello VMM sunucusu düzgün ayarlandığından emin olmanız gerekir. Hello sağ VMM sürümü ve Bulutlar ayarlanır çalışmakta olduğunuzdan emin dahildir.
**Hyper-V** | Windows Server 2012 R2 çalıştıran hello şirket içi sitede en az bir Hyper-V konak sunucusu veya üzeri | En az bir Hyper-V server çalıştıran en az hello kaynak ve hedef siteleri hello en son güncelleştirmeleri içeren Windows Server 2012 ve bağlı toohello Internet.<br/><br/> Merhaba Hyper-V sunucularının, VMM Bulutu konak grubunda olması gerekir. | En az bir Hyper-V server çalıştıran en az hello kaynak ve hedef siteleri hello en son güncelleştirmeleri içeren Windows Server 2012 ve bağlı toohello Internet.<br/><br/> VMM Bulutu konak grubunda Hello Hyper-V sunucularında bulunması gerekir. |
**Sanal makineler** | Merhaba kaynak Hyper-V konak sunucusunda en az bir VM | VMM Bulutu hello kaynağındaki hello Hyper-V konak sunucusunda en az bir VM | En az bir VM VMM bulut hello kaynağındaki hello Hyper-V konak sunucusunda. |  Sanal makineleri çoğaltma tooAzure Azure sanal makine önkoşulları uymalıdır
**Azure hesabı** | Bir Azure hesabı ve aboneliği toohello Site Recovery hizmeti gerekir. | Bir Azure hesabı ve aboneliği toohello Site Recovery hizmeti gerekir. | NA | Bir hesabınız yoksa ücretsiz deneme sürümü ile başlayın.
**Azure depolama alanı** | Coğrafi çoğaltma özelliğinin etkin olduğu bir Azure depolama hesabına abone olmanız gerekir. | Coğrafi çoğaltma özelliğinin etkin olduğu bir Azure depolama hesabına abone olmanız gerekir. | NA | Merhaba hesabı olmalıdır hello hello Azure Site kurtarma kasasıyla aynı bölgede ve hello ile ilişkili aynı abonelik.
**Ağ** | Ağ eşleme tooensure üzerinde devreden tüm makineler aynı Azure ağ hello ayarlama tooeach bulundukları hangi kurtarma planı yedeklemiş diğer bağlanabilir. Ayrıca bir ağ geçidi yapılandırmak, hello hedef Azure ağını sanal makineleri tooother şirket içi sanal makinelere bağlanabilir. Ayarlamazsanız yalnızca aynı kurtarma planında bağlanabilir hello yük devri makineler eşleme ağ. | NA |  <br/><br/>Yük devretme sonrasında sanal makineleri bağlı tooappropriate ağlardır ve çoğaltma sanal makinelerini Hyper-V ana bilgisayar sunucuları üzerinde en iyi şekilde yerleştirilir ağ eşlemesi tooensure ayarlayın. Ağ yapılandırmazsanız çoğaltılmış makineler eşleme olmayacak bağlı tooany VM ağı yük devretme sonrasında. |  VMM ile ağ eşlemesi tooset toomake VMM mantıksal ve VM ağları doğru şekilde yapılandırıldığından emin olmanız gerekir.
**Sağlayıcılar ve aracılar** | Dağıtım sırasında VMM sunucularına Azure Site Recovery sağlayıcısı hello yükleyeceksiniz. VMM bulutlarındaki Hyper-V sunucularında, hello Azure kurtarma Hizmetleri aracısını yüklemeniz. | Dağıtım sırasında hello Azure Site Recovery sağlayıcısı ve hello Azure kurtarma Hizmetleri aracısını hello Hyper-V konak sunucusu veya kümeye yüklemeniz| Dağıtım sırasında VMM sunucularına Azure Site Recovery sağlayıcısı hello yükleyeceksiniz. VMM bulutlarındaki Hyper-V sunucularında, hello Azure kurtarma Hizmetleri aracısını yüklemeniz. | Sağlayıcıları ve aracıları bağlanmak tooSite kurtarma hello üzerinden şifrelenmiş bir HTTPS bağlantısı kullanarak Internet. Tooadd güvenlik duvarı özel durumlarını gerek yoktur veya hello sağlayıcı bağlantısı için özel bir proxy oluşturun.
**İnternet bağlantısı** | Yalnızca hello VMM sunucusu bir Internet bağlantısı gereklidir | Yalnızca hello Hyper-V ana bilgisayar sunucuları internet bağlantısı gerekir | Yalnızca VMM sunucuları için İnternet bağlantısı gereklidir | Sanal makineler yüklü herhangi bir şey gerekmez ve toohello doğrudan bağlanma Internet.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>VMware sanal makineleri veya fiziksel sunucularını koruma

VMware sanal makinelerini veya Windows/Linux fiziksel sunucularını korumaya yönelik birkaç dağıtım seçeneği mevcuttur. Bunları tooAzure veya tooa ikincil veri merkezine çoğaltabilirsiniz. Her dağıtım için farklı gereksinimler vardır.

**Gereksinim** | **Çoğaltma VMware VM'ler/fiziksel sunucular tooAzure)** | * **VMware VM'ler/fiziksel sunucular toosecondary site Çoğalt**  
---|---|---
**Birincil site** | **İşlem sunucusu**: ayrılmış bir Windows sunucusu (fiziksel veya sanal) | **İşlem sunucusu**: ayrılmış bir Windows sunucusu (fiziksel veya VMware sanal makinesi)<br/><br/>  
**Şirket içi ikincil site** | NA | **Yapılandırma sunucusu**: ayrılmış bir Windows sunucusu (fiziksel veya sanal) <br/><br/> **Ana hedef sunucu**: ayrılmış bir sunucu (fiziksel veya sanal). Windows tooprotect Windows makine ya da Linux tooprotect Linux yapılandırın.
**Azure** | **Abonelik**: Merhaba Site Recovery hizmeti bir aboneliği gerekir. <br/><br/> **Depolama hesabı**: Coğrafi çoğaltmanın etkin olduğu bir depolama hesabınızın olmalıdır. Merhaba hesabı olmalıdır hello hello Site Recovery kasasıyla aynı bölgede ve hello ile ilişkili aynı abonelik. <br/><br/> **Yapılandırma sunucusu**: hello yapılandırma sunucusu Azure VM olarak tooset gerekir <br/><br/> **Ana hedef sunucusu**: hello ana hedef sunucu bir Azure VM olarak tooset gerekir <br/><br/> Windows tooprotect Windows makine ya da Linux tooprotect Linux yapılandırın.<br/><br/> **Azure sanal ağı**: hangi hello üzerinde yapılandırma sunucusu ve ana hedef sunucusu dağıtılacak bir Azure sanal ağınızın olması gerekir. Hello olmalıdır aynı abonelikte ve bölgede hello Azure Site Recovery kasası | NA  
**Sanal makineler/fiziksel sunucular** | En az bir VMware sanal makinesi veya fiziksel Windows/Linux sunucusu.<br/><br/>Dağıtım sırasında her makinede Mobility hizmeti hello yüklenecek| En az bir VMware VM veya fiziksel Windows/Linux sunucusu.<br/><br/> Dağıtım sırasında hello birleşik aracı her makineye yüklenir.




## <a name="azure-virtual-machine-requirements"></a>Azure sanal makine gereksinimleri

Site Recovery tooreplicate sanal makineler ve Azure tarafından desteklenen herhangi bir işletim sistemini çalıştıran fiziksel sunucuları dağıtabilirsiniz. Buna çoğu Windows ve Linux sürümü dahildir. Toomake emin olun, şirket içi sanal makineleri tooprotect istediğiniz Azure gereksinimlerine uygun ihtiyacınız olacak.


## <a name="optimizing-your-deployment"></a>Dağıtımınızı en iyi duruma getirme

En iyi duruma getirme ve dağıtımınız ölçeklendirmek ipuçları toohelp aşağıdaki hello kullanın.

- **İşletim sistemi birimi boyutu**: işletim sistemi birimi bir sanal makine tooAzure hello çoğaltmak zaman 1 TB değerinden küçük olmalıdır. Bu daha fazla birim varsa, dağıtım başlamadan önce el ile bunları tooa farklı disk taşıyabilirsiniz.
- **Veri disk boyutu**: too32 veri diski bir sanal makinede, her en fazla 1 TB çalışır duruma getirdikten tooAzure çoğaltıyorsanız. Yaklaşık 32 TB’lık bir sanal makineyi etkili bir şekilde çoğaltabilir ve yük devredebilirsiniz.
- **Kurtarma planı sınırları**: Site Recovery toothousands sanal makinelerin ölçeklendirilebilir. Kurtarma planları, size bir kurtarma planı too50 makinelerinizde hello sayısını sınırlamak için birlikte yük devri uygulamalar için bir model olarak tasarlanmıştır.
- **Azure hizmet sınırları**: Her Azure aboneliği, çekirdeklere, bulut hizmetlerine vb. yönelik varsayılan sınırlamalarla sunulur. Kaynakları bir test yük devretme toovalidate hello kullanılabilirliği aboneliğinizde çalıştırmanızı öneririz. Bu limitleri Azure desteği aracılığıyla değiştirebilirsiniz.
- **Kapasite planlama**: Ölçekleme ve performans için planlama.
- **Çoğaltma bant genişliği**: Çoğaltma bant genişliği azaldıysa şunları unutmayın:
    - **ExpressRoute**: Site Recovery, Riverbed gibi Azure ExpressRoute ve WAN iyileştiricileri ile birlikte çalışır.
    - **Çoğaltma trafiği**: Site Recovery kullanan yalnızca veri bloklarını kullanarak akıllı bir ilk çoğaltma gerçekleştirir ve tüm VHD hello değil. Devam eden çoğaltma sırasında yalnızca değişiklikler çoğaltılır.
    - **Ağ trafiğini**: çoğaltma için Windows QoS hello hedef IP adresi ve bağlantı noktası dayalı bir ilke ayarı kullanılan ağ trafiğini denetleyebilirsiniz.  Site Recovery tooAzure çoğaltıyorsanız ayrıca hello Azure yedekleme Aracısı'nı kullanma. Bu aracı için azaltma yapılandırabilirsiniz.
- **RTO**: yük devretme testi çalıştırmak ve hello Site Recovery işleri tooanalyze ne kadar zaman onu görünümü sürer toocomplete hello işlemleri beklediğiniz Site Recovery ile toomeasure hello kurtarma süresi hedefi (RTO) istiyorsanız öneririz. Merhaba tooAzure çalıştırma işlemini gerçekleştiriyorsanız, Azure automation ve Kurtarma ile tümleştirerek tüm el ile gerçekleştirilen eylemleri otomatikleştirmek öneririz en iyi RTO planlar.
- **RPO**: Site Recovery tooAzure çoğalttığınızda yakın zaman uyumlu kurtarma noktası hedefi (RPO) destekler. Bu seçenek, veri merkeziniz ile Azure arasında yeterli bant genişliği olduğunu varsayar.
