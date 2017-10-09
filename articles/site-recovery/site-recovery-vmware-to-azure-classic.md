---
title: "aaaReplicate VMware Vm'lerini ve fiziksel sunucuları tooAzure hello Klasik portalı | Microsoft Docs"
description: "Bu makalede nasıl toodeploy Azure Site Recovery tooorchestrate çoğaltma, yük devretme ve kurtarma işlemlerini şirket içi VMware sanal makinelerini ve Windows/Linux fiziksel sunucuları tooAzure açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>VMware sanal makineleri ve fiziksel sunucuları tooAzure Azure Site Recovery ile çoğaltma
> [!div class="op_single_selector"]
> * [Hello Azure portalı](site-recovery-vmware-to-azure.md)
> * [Merhaba Klasik portal](site-recovery-vmware-to-azure-classic.md)
> * [Merhaba Klasik portal (eski)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Hello Azure Site Recovery hizmeti çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenleyerek tooyour iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar. Makineler çoğaltılmış tooAzure veya tooa ikincil şirket içi veri merkezi olabilir. Hızlı bir genel bakış için bkz: [Azure Site Recovery nedir?](site-recovery-overview.md).

## <a name="overview"></a>Genel Bakış
Bu makalede nasıl yapılır:

* **VMware sanal makineleri tooAzure çoğaltmak**: Site Recovery dağıtımı toocoordinate çoğaltma, yük devretme ve kurtarma şirket içi VMware sanal makineleri tooAzure depolama.
* **Fiziksel sunucuları tooAzure çoğaltmak**: Azure Site Recovery dağıtımı toocoordinate çoğaltma, yük devretme ve şirket içi fiziksel Windows ve Linux sunucuları tooAzure kurtarılması.

> [!NOTE]
> Bu makalede nasıl tooreplicate tooAzure. Tooreplicate VMware Vm'leri veya Windows/Linux fiziksel sunucuları tooa ikincil veri merkezine istiyorsanız, bkz: [Site kurtarma VMware tooVMware](site-recovery-vmware-to-vmware.md).
>
>

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Gelişmiş dağıtım
Bu makalede hello Klasik Azure portalı Gelişmiş bir dağıtımı için yönergeler içerir. Tüm yeni dağıtımlar için bu sürümünü kullanmanızı öneririz. Tarafından zaten dağıttıktan sonra önceki eski sürümü Merhaba kullanarak, toohello yeni sürümü geçirmek öneririz. Geçiş hakkında daha fazla bilgi için bkz: [Site kurtarma VMware tooAzure Klasik eski](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

Gelişmiş Merhaba, önemli bir güncelleştirme dağıtımıdır. Merhaba geliştirmeler yaptık bir özeti aşağıda verilmiştir:

* **Hiçbir altyapı azure'da Vm'leri**: verilerini çoğaltır doğrudan tooan Azure depolama hesabı. Ayrıca, var. hiç gerek tooset herhangi bir altyapı VM'ler (yapılandırma sunucusu veya ana hedef sunucusu gibi) yukarı çoğaltma ve yük devretme için hello eski dağıtımda gerektiğinde  
* **Birleşik yükleme**: tek bir yüklemede basit kurulumu ve şirket içi bileşenleri için ölçeklenebilirlik sağlar.
* **Dağıtımınızın güvenliğini**: tüm trafiği şifrelenir ve çoğaltma yönetim iletişimleri HTTPS 443 üzerinden gönderilir.
* **Kurtarma noktaları**: desteği kilitlenme ve uygulamaları tutarlı kurtarma noktaları Windows ve Linux ortamlar için ve her ikisi de tek bir VM ve çoklu VM tutarlı yapılandırmaları için destek.
* **Yük devretme sınamasını**: etkilemeden üretim veya çoğaltma duraklatma olmadan benzer test yük devretme tooAzure desteği.
* **Planlanmamış yük devretme**: Gelişmiş seçeneği tooautomatically ile planlanmamış yük devretme tooAzure desteği önce yük devretme sanal makineleri kapatın.
* **Yeniden çalışma**: toohello delta değişiklikleri geri yalnızca, çoğaltılan tümleşik geri dönme şirket içi site.
* **vSphere 6.0**: sınırlı VMware vSphere 6.0 dağıtımları için destek.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Site Recovery sanal makineleri ve fiziksel sunucuları korumaya nasıl yardımcı olur?
* VMware kurumsal iş yükleri ve VMware sanal makinelerde çalışan uygulamaların site dışındaki korumaları tooprotect Azure yapılandırabilirler. Sunucu yöneticilerinin, fiziksel şirket içi Windows ve Linux sunucuları tooAzure çoğaltabilirsiniz.
* Hello Azure Site Kurtarma Konsolu basit kurulum ve yönetim çoğaltma, yük devretme ve kurtarma işlemleri için tek bir konum sağlar.
* Bir vCenter sunucusu tarafından yönetilen bir VMware sanal makineleri çoğaltmak, Site Recovery bu sanal makineleri otomatik olarak bulabilir. Makineler ESXi ana bilgisayarda varsa, Site Recovery hello ana bilgisayarda sanal makineleri bulur.
* Şirket içi altyapı tooAzure kolay yük devretme çalıştırırsanız, başarısız olabilir () Azure tooVMware VM sunuculardan hello şirket içi siteye geri.
* Birden fazla makine arasında katmanlı uygulama iş yüklerini grup kurtarma planlarını yapılandırabilirsiniz. Bu planlara başarısız olursa, Site Recovery aynı iş yükleri olabilir hello çalışan makineler birlikte tooa tutarlı veri noktası kurtarılan çoklu VM tutarlılığı sağlar.

## <a name="supported-operating-systems"></a>Desteklenen işletim sistemleri
### <a name="windows-64-bit-only"></a>Windows (yalnızca 64 bit)
* Windows Server 2008 R2 SP1 +
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (yalnızca 64 bit)
* Red Hat Enterprise Linux 7.2 6.7 ve 7.1
* CentOS 6.5, 6.6, 6.7, 7.0, 7.1 ve 7.2
* Oracle 6.4 ve 6.5 çalışan ya da hello Red Hat Enterprise Linux uyumlu çekirdek veya kesilemeyen kurumsal çekirdek sürüm 3 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>Senaryo mimarisi
Senaryo Bileşenleri:

* **Bir şirket içi yönetim sunucusu**: hello yönetim sunucusu, Site Recovery bileşenlerini çalıştıran:
  * **Yapılandırma sunucusu**: iletişimi düzenler ve veri çoğaltma ve kurtarma işlemlerini yönetir.
  * **İşlem sunucusu**: çoğaltma ağ geçidi olarak davranır. Korumalı kaynak makinelerden veri aldığı; önbelleğe alma, sıkıştırma ve şifreleme iyileştirir; ve gönderir çoğaltma veri tooAzure depolama. Ayrıca Mobility hizmeti tooprotected makinelere göndermeli yüklemesini işler ve VMware vm'lerinin otomatik bulma işlemini gerçekleştirir.
  * **Ana hedef sunucusu**: Azure'dan yeniden çalışma sırasında çoğaltma verilerini işler.
    Dağıtımınız yalnızca işlem sunucusu tooscale davranan bir yönetim sunucusu da dağıtabilirsiniz.
* **Mobility hizmeti hello**: Bu bileşen tooreplicate tooAzure istediğiniz her makinede (VMware VM veya fiziksel sunucusu) dağıtılır. Merhaba makinede veri Yazar yakalar ve bunları toohello işlem sunucusuna iletir.
* **Azure**: herhangi bir Azure sanal makineleri toohandle çoğaltma ve yük devretme toocreate gerekmez. Veri Yönetimi Hello Site Recovery hizmeti işler ve verileri doğrudan tooAzure depolama çoğaltır. Yalnızca Yük devretme tooAzure meydana geldiğinde çoğaltılan Azure Vm'leri çalışmaya otomatik olarak başlar. Ancak, Azure toohello şirket içi sitesinden geri toofail istiyorsanız, işlem sunucusu olarak bir Azure VM tooact yukarı tooset gerekir.

Bu bileşenlerin nasıl etkileşim (Henry Robalino tarafından oluşturulan) grafiği aşağıdaki hello gösterir:

![Bileşen mimarisi](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Kapasite planlaması
Kapasite planlama zaman toothink hakkında gerekenler şöyledir:

* **Merhaba kaynak ortamı**: kapasite planlaması veya hello VMware altyapı ve kaynak makine gereksinimleri.
* **Merhaba yönetim sunucusu**: hello içi Site Recovery bileşenlerini çalıştıran yönetim sunucuları için planlama.
* **Ağ bant genişliğini kaynak tootarget ile**: hello kaynak ve Azure arasında çoğaltma için gereken ağ bant genişliğini planlama.

### <a name="source-environment-considerations"></a>Kaynak ortamı konuları
* **Maksimum günlük değişim oranı**: bir korumalı makine yalnızca bir işlem sunucusu kullanabilirsiniz. Tek bir işlem sunucusu TB'lık veriyi değiştirme günde too2 yukarı işleyebilir. Bu nedenle, 2 TB hello maksimum günlük veri korumalı bir makine için desteklenen oranı değiştirmektir.
* **En yüksek verimlilik**: çoğaltılmış bir makineden Azure depolama hesabında tooone ait olabilir. Standart depolama hesabı 20.000 istekleri saniye başına maksimum işleyebilir ve bir kaynak makine too20 000 arasında hello IOPS sayısını tutmanızı öneririz. Örneğin, kaynak makine 5 disklerle varsa ve her disk hello kaynağında 120 IOPS (8 KB boyutu) oluşturur, bu hello Azure başına 500 disk IOPS sınırı içinde olacaktır. Merhaba gerekli depolama hesabı sayısı toplam kaynak IOP/20, 000 =.

### <a name="management-server-considerations"></a>Yönetim sunucusu değerlendirmeleri
Merhaba yönetim sunucusu veri en iyi duruma getirme, çoğaltma ve yönetim işleyen Site Recovery bileşenlerini çalıştırır. Korumalı makineler üzerinde çalışan tüm iş yükleri arasında mümkün toohandle hello günlük değişikliği oranı kapasite olmalıdır ve veri tooAzure depolama çoğaltma yeterli bant genişliği toocontinuously sahiptir. Bu avantajlar şunlardır:

* Merhaba işlem sunucusu korunan makinelerden çoğaltma verilerini alıp ve önbelleğe alma, sıkıştırma ve şifreleme tooAzure göndermeden önce iyileştirir. Merhaba yönetim sunucusu, bu görevleri yeterli kaynakları tooperform olması gerekir.
* Merhaba işlem sunucusu disk tabanlı önbelleği kullanır. Ayrı önbelleği disk 600 GB veya daha fazla toohandle veri değişikliklerini ağ sorununu veya kesinti hello olayda depolanan öneririz. Dağıtım sırasında hello önbellek en az 5 GB depolama alanı kullanılabilir olan herhangi bir sürücüde yapılandırabilirsiniz, ancak 600 GB hello minimum önerilir.
* En iyi uygulama, bu hello yönetim sunucusu üzerinde hello bulunuyorsa olan öneririz aynı ağ ve LAN kesimi olarak hello tooprotect istediğiniz makineler. Farklı bir ağ, ancak tooprotect L3 ağ görünürlük tooit olmalıdır istediğiniz makineler üzerinde bulunabilir.

Boyutu önerileri hello yönetim sunucusu için aşağıdaki tablonun hello özetlenmiştir:

| **Yönetim sunucusu CPU** | **Bellek** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler** |
| --- | --- | --- | --- | --- |
| 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek) |16 GB |300 GB |500 GB veya daha az |Bu ayarları tooreplicate yönetim sunucusuyla 100'den az makineleri dağıtın. |
| 12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) |18 GB |600 GB |500 GB too1 TB |Bir yönetim sunucusu bu ayarları tooreplicate 100-150 makinelerle dağıtın. |
| 16 Vcpu (2 yuva * 2,5 GHz @ 8 çekirdek) |32 GB |1 TB |1 TB too2 TB |Bir yönetim sunucusu bu ayarları tooreplicate 150-200 makinelerle dağıtın. |
| Başka bir işlem sunucusu Dağıt | | |> 2 TB |Ek işlem sunucusu 200'den fazla makineleri çoğaltma yapıyorsanız ya da hello günlük verileri değiştirirseniz oranı 2 TB aştığında dağıtın. |

Konumlar:

* Her kaynak makine 3 100 GB disk ile yapılandırılır.
* 8 SAS sürücüleri 10.000 RPM Kıyaslama depolanmasını RAID 10 ile için önbellek disk ölçümleri kullandık.

### <a name="network-bandwidth-from-source-tootarget"></a>Ağ bant genişliğini kaynak tootarget ile
Hello kullanarak ilk çoğaltma ve değişim çoğaltması için gerekli olacak hello bant genişliğini hesaplamak emin olun [kapasite planlayıcısı aracı](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Çoğaltma için kullanılan bant genişliği azaltma
VMware çoğaltılan trafiği tooAzure belirli işlem sunucusu üzerinden gider. Site Recovery çoğaltma bu sunucu üzerinde aşağıdaki gibi kullanılabilir hello bant genişliğini azaltmak:

1. Merhaba ana yönetim sunucusunda Microsoft Azure Backup MMC ek bileşenini Hello açın veya bir yönetim sunucusu üzerinde ek çalışan işlem sunucuları sağlandı. Varsayılan olarak, Microsoft Azure yedekleme için bir kısayol hello masaüstünde oluşturulur. Veya, C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin içinde yolunda bulabilirsiniz.
2. Merhaba ek bileşeninde, tıklatın **özelliklerini değiştirme**.

    ![Bant genişliği Özellikleri Değiştir kısıtlama](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Merhaba üzerinde **azaltma** sekmesinde, Site Recovery çoğaltma için kullanılan ve geçerli zamanlama hello hello bant genişliğini belirtin.

    ![Çoğaltma bant genişliği azaltma](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

PowerShell kullanarak azaltma de ayarlayabilirsiniz. Örnek aşağıda verilmiştir:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Bant genişliği kullanımını en üst düzeye çıkarma
Çoğaltma için Azure Site Recovery tarafından kullanılan tooincrease hello bant genişliği toochange bir kayıt defteri anahtarı gerekir.

Merhaba aşağıdaki anahtar denetimleri çoğaltırken kullanılan disk çoğaltma başına iş parçacığı sayısını hello:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 Fazla sağlanan bir ağda, bu kayıt defteri anahtarı kendi varsayılan değerlerini değiştirilen toobe gerekir. En fazla 32 destekliyoruz.  

Ayrıntılı kapasite planlaması hakkında daha fazla bilgi için bkz: [Site Recovery kapasite Planlayıcısı](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Ek işlem sunucuları
Tooprotect gerekiyorsa 200'den fazla makine ya da günlük değişikliği hızınızı 2 TB ek sunucular toohandle hello yük ekleyebilirsiniz daha büyük. tooscale çıkış şunları yapabilirsiniz:

* Yönetim sunucuları Hello sayısını artırın. Örneğin, iki yönetim sunucuları ile too400 makineler koruyabilirsiniz.
* Ek işlem sunucusu ekleyin ve bu toohandle trafiği yerine (veya ek olarak) hello yönetim Sunucusu'nu kullan.

Bu tabloda bir senaryoda açıklanmıştır:

* Merhaba özgün yönetim sunucusu toouse yalnızca bir yapılandırma sunucusu olarak ayarlayın.
* Bir ek işlem sunucusu ayarlayın.
* Korumalı sanal makineleri toouse hello ek işlem sunucusu yapılandırın.
* Her korumalı kaynak makine üç 100 GB disk ile yapılandırılır.

| **Özgün yönetim sunucusu**<br/><br/>(yapılandırma sunucusu) | **Ek işlem sunucusu** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler** |
| --- | --- | --- | --- | --- |
| 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 16 GB RAM |4 Vcpu (2 yuva * 2,5 GHz @ 2 Çekirdek), 8 GB RAM |300 GB |250 GB veya daha az |85 veya daha az makineleri çoğaltabilirsiniz. |
| 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 16 GB RAM |8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 12 GB RAM |600 GB |250 GB too1 TB |85 150 makineleri çoğaltabilirsiniz. |
| 12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek), 18 GB RAM |12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) 24 GB RAM |1 TB |1 TB too2 TB |150-225 makineleri çoğaltabilirsiniz. |

Sunucularınızın ölçeklendirme nasıl büyütme veya genişleme modeli için tercihinizi bağlıdır. Birkaç Gelişmiş Yönetim ve işlem sunucuları dağıtarak ölçeği veya daha az kaynak ile daha fazla sunucu dağıtarak ölçeğini. Örneğin: tooprotect 220 makineler gerekiyorsa, hello aşağıdakilerden birini yapabilirsiniz:

* Merhaba özgün yönetim sunucusu 12 Vcpu'lar ve 18 GB RAM yapılandırın. Bir ek işlem sunucusu 12 Vcpu'lar ve 24 GB RAM yapılandırın. Korumalı makineler toouse yalnızca hello ek işlem sunucusu yapılandırın.
* İki yönetim sunucuları (2 x 8 Vcpu, 16 GB RAM) ve iki ek işlem sunucusu (1 x 8 Vcpu'lar ve 4vCPUs 1 toohandle 135 + 85 (220) makineler x) yapılandırın. Korumalı makineler toouse yalnızca hello ek işlem sunucularını yapılandırın.

Merhaba yönergeleri izleyin [ek işlem sunucusu dağıtın](#deploy-additional-process-servers) tooset bir ek işlem sunucusu.

## <a name="before-you-start-deployment"></a>Dağıtıma başlamadan önce
Merhaba aşağıdaki tablolarda bu senaryoyu dağıtmak için hello önkoşullar özetlenmektedir.

### <a name="azure-prerequisites"></a>Azure önkoşulları
| **Önkoşul** | **Ayrıntılar** |
| --- | --- |
| **Azure hesabı** |Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Site Recovery fiyatlandırması hakkında daha fazla bilgi için bkz: [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Azure depolama alanı** |Bir Azure depolama hesabı toostore çoğaltılmış verileri gerekir. Çoğaltılan veriler Azure depolama alanında depolanır ve yük devretme durumunda Azure Vm'leri çalışmaya başlar. <br/><br/>[Standart coğrafi olarak yedekli depolama hesabınızın](../storage/storage-redundancy.md#geo-redundant-storage) olması gerekir. Merhaba hesabı olmalıdır hello hello Site Recovery hizmeti ile aynı bölgeye ve hello ile ilişkili aynı abonelik. Çoğaltma toopremium depolama hesapları şu anda desteklenmiyor ve kullanılmamalıdır.<br/><br/>Merhaba kullanılarak oluşturulan taşıma depolama hesapları desteklemiyoruz [Azure portal](../storage/storage-create-storage-account.md) kaynak grupları arasında. Daha fazla bilgi için bkz: [giriş tooMicrosoft Azure Storage](../storage/storage-introduction.md).<br/><br/> |
| **Azure ağı** |Azure VM'ler bağlanacak bir Azure sanal ağı gerekir toowhen yük devretme oluşur. Hello Azure sanal ağı hello olmalıdır hello Site Recovery kasasıyla aynı bölgede.<br/><br/>toofail yük devretme tooAzure sonra tekrar gereksinim duyduğunuz bir VPN bağlantısı (veya Azure ExpressRoute) ayarlanan hello Azure ağ toohello şirket içi siteden. |

### <a name="on-premises-prerequisites"></a>Şirket içi önkoşullar
| **Önkoşul** | **Ayrıntılar** |
| --- | --- |
| **Yönetim sunucusu** |Bir sanal makine ya da fiziksel sunucu üzerinde çalışan bir şirket içi Windows 2012 R2 sunucusu gerekir. Tüm hello şirket içi Site Recovery bileşenlerini bu yönetim sunucusuna yüklenir.<br/><br/> Merhaba sunucusu yüksek oranda kullanılabilir bir VMware VM olarak dağıtmak öneririz. Yeniden çalışma toohello şirket içi Azure her zaman, sanal makineleri veya fiziksel sunucular üzerinden başarısız bağımsız olarak tooVMware VM'ler sitedir. VMware VM olarak hello Yönetim Sunucusu yapılandırmazsanız, bir VMware VM tooreceive yeniden çalışma trafiği olarak tooset ayrı ana hedef sunucusu gerekir.<br/><br/>Merhaba sunucu bir etki alanı denetleyicisi olmaması gerekir.<br/><br/>Merhaba sunucunun bir statik IP adresi olmalıdır.<br/><br/>Merhaba sunucunun Hello ana bilgisayar adı 15 karakter uzunluğunda olmalıdır veya daha az.<br/><br/>yalnızca Hello işletim sistemi yerel ayarı İngilizce olmalıdır.<br/><br/>Merhaba yönetim sunucusunun Internet erişimi gerektirir.<br/><br/>Giden hello sunucusundan gibi erişmeniz: hello Site Recovery bileşenlerini (toodownload MySQL); Kurulumu sırasında HTTP 80 üzerinde geçici erişim çoğaltma yönetimi için HTTPS 443 üzerinde devam eden giden erişim; çoğaltma trafiği (Bu bağlantı noktası değiştirilebilir) için HTTPS 9443 üzerinde devam eden giden erişim.<br/><br/> Bu URL'leri hello yönetim sunucusundan erişilebilir olduğundan emin olun: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>-https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.MySQL.com/Get/Archives/MySQL-5.5/MySQL-5.5.37-Win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>IP adresi tabanlı güvenlik duvarı kuralları hello sunucuda varsa, hello kuralları iletişim tooAzure izin verdiğinden emin olun. Tooallow hello gereksinim [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653) ve hello HTTPS (443 numaralı) bağlantı noktası. Merhaba aboneliğinizin Azure bölgesi ve Batı ABD ayrıca toowhitelist IP adres aralıklarını gerekir. Merhaba URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") MySQL yüklemek için değil. |
| **VMware vCenter/ESXi ana bilgisayar** |ESX/ESXi sürüm 6.0, 5.5 veya 5.1 hello en son güncelleştirmeleri ile çalışan, VMware sanal makineleri yönetme bir veya daha fazla VMware vSphere ESX/ESXi hiper gerekir.<br/><br/> Bir VMware vCenter server toomanage ESXi konakları dağıtmanızı öneririz. VCenter sürüm 6.0 veya 5.5 hello en son güncelleştirmeleri ile çalışmalıdır.<br/><br/>Site Recovery yeni vCenter desteklemez ve vSphere 6.0 özellikleri gibi vCenter VMotion'ı, sanal birimler ve depolama DRS arası unutmayın. Site kurtarma desteği de 5.5 sürümünde kullanılabilir sınırlı toofeatures değil. |
| **Korumalı makineler** |**Azure**<br/><br/>Tooprotect uygun ile istediğiniz makineleri [Azure önkoşulları](site-recovery-prereq.md) Azure sanal makineleri oluşturmak için.<br><br/>Yük devretme sonrasında Azure Vm'lerinin tooconnect toohello istiyorsanız, tooenable Uzak Masaüstü bağlantıları hello Yerel Güvenlik Duvarı'nda gerekir.<br/><br/>Korumalı makinelerdeki bağımsız disk kapasitesinin 1023 GB'tan fazla olmaması gerekir. Bir VM yukarı too64 diskleri (Bu nedenle too64 TB) olabilir. 1 TB'den büyük olan diskler varsa, veritabanı çoğaltması SQL Server Always On veya Oracle Data Guard gibi kullanmayı düşünün.<br/><br/>Bileşen yüklemesi için hello yükleme sürücüsünde kullanılabilir alan en az 2 GB.<br/><br/>Paylaşılan disk konuk kümeleri desteklenmez. Kümelenmiş bir dağıtımınız varsa, veritabanı çoğaltması SQL Server Always On veya Oracle Data Guard gibi kullanmayı düşünün.<br/><br/>Birleşik Genişletilebilir Bellenim Arabirimi (UEFI) / Genişletilebilir Bellenim EFI önyükleme desteklenmez.<br/><br/>Makine adı 1 ile 63 karakter arasında (harf, rakam ve kısa çizgi) içermelidir. Merhaba adı bir harf veya sayı ile başlamalı ve bir harf veya sayı ile bitmelidir. Bir makine korunduktan sonra hello Azure adını değiştirebilirsiniz.<br/><br/>**VMware Vm'leri**<br/><br>Tooinstall VMware vSphere Powerclı 6.0 gerekir. Merhaba yönetim sunucusunda (yapılandırma sunucusu).<br/><br/>VMware Vm'leri istediğiniz tooprotect VMware araçları yüklü ve çalışıyor olması gerekir.<br/><br/>NIC ekibi oluşturma Hello kaynak VM varsa, dönüştürülür tooa tek NIC sonra Yük devretme tooAzure.<br/><br/>Korumalı VM'lerin bir iSCSI diski varsa, Site Recovery dönüştürür hello hello VM tooAzure başarısız olduğunda bir VHD dosyasına VM iSCSI disk korumalı. İSCSI hedef hello Azure VM tarafından erişilebilir değilse, tooiSCSI hedef bağlanmak ve temelde iki disk bkz: hello VHD disk hello Azure VM ve hello kaynak iSCSI disk üzerinde. Bu durumda, toodisconnect gerekir hello üzerinde görünür hello iSCSI hedef başarısız oldu-üzerinden Azure VM.<br/><br/>Merhaba VMware kullanıcı izinleri hakkında daha fazla bilgi için Site kurtarma, bkz: gereken [VMware vCenter erişim izinlerini](#vmware-permissions-for-vcenter-access).<br/><br/> **Windows Server makinelerde (VMware VM veya fiziksel sunucu)**<br/><br/>Merhaba sunucusu, desteklenen bir 64-bit işletim sistemi çalıştırıyor olması: Windows Server 2012 R2, Windows Server 2012 veya Itanium tabanlı sistemler için Windows Server 2008 R2 ile en az SP1.<br/><br/>Merhaba işletim sistem C sürücüsünde yüklenmelidir ve hello işletim sistemi diski Windows temel disk olması gerekir. (Merhaba işletim sistemi bir Windows dinamik diske yüklenmesi gerekir.)<br/><br/>Windows Server 2008 R2 makineler için .NET Framework 3.5.1 yüklü toohave gerekir.<br/><br/>Tooprovide yönetici hesabı gerekir (Merhaba Windows makinesinde yerel yönetici olması gerekir) Windows sunucularında hello anında yükleme hello Mobility hizmeti için. Merhaba hesap bir etki alanı dışı hesabıdır verdiyse, toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir. Daha fazla bilgi için bkz: [gönderme yüklemesi ile Merhaba mobilite hizmeti yükleme](#install-the-mobility-service-with-push-installation).<br/><br/>Site Kurtarma ile RDM diski Vm'leri destekler. Merhaba özgün kaynak VM ve RDM diski mevcutsa, yeniden çalışma sırasında Site Recovery hello RDM diski yeniden kullanır. Yeniden çalışma sırasında kullanılabilir durumda değilse, Site Recovery her disk için yeni bir VMDK dosyasını oluşturun.<br/><br/>**Linux makineler**<br/><br/>Desteklenen bir 64-bit işletim sistemi gerekir: Red Hat Enterprise Linux 6.7; Centos 6.5, 6.6 veya 6.7; Oracle Enterprise Linux 6.4 veya hello Red Hat uyumlu çekirdek veya kesilemeyen kurumsal çekirdek sürüm 3 (UEK3); çalışan 6.5 SUSE Linux Enterprise Server 11 SP3.<br/><br/>/ etc/hosts dosyaları korumalı makinelerdeki tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin giriş içermelidir. <br/><br/>Tooconnect tooan Azure sanal makinesini isterseniz korunan hello makine hello Secure Shell hizmetinin sistem önyüklemede otomatik olarak toostart ayarlanır ve güvenlik duvarı kuralları izin sağlamak bir Secure Shell istemcisi kullanarak (ssh), yük devretme sonrasında Linux çalıştıran bir ssh bağlantı tooit.<br/><br/>Koruma yalnızca etkinleştirilebilir Linux makineler için depolama aşağıdaki hello ile: dosya sistemi (EXT3, ETX4, ReiserFS, XFS); Çok yollu yazılım-aygıtı Eşleyici (çok yollu); Birim Yöneticisi (LVM2). HP CCISS denetleyicisi depolama ile fiziksel sunucuları desteklenmez. Merhaba ReiserFS dosya sistemi yalnızca SUSE Linux Enterprise Server 11 SP3 üzerinde desteklenir.<br/><br/>Site Kurtarma ile RDM diski Vm'leri destekler. Linux için yeniden çalışma sırasında Site Recovery hello RDM diski yeniden kullanmaz. Bunun yerine, karşılık gelen her RDM diski için yeni bir VMDK dosyası oluşturur. |

Yalnızca bir Linux VM için: hello VMware VM yapılandırma parametrelerinin hello hello disk.enableUUID=true ayarını belirleyin emin olun. Bu satır mevcut değilse, bunu ekleyin. Bu gerekli tooprovide tutarlı UUID toohello VMDK, böylelikle doğru bağlar. Merhaba VM içi kullanılabilir olsa bile, bu ayar olmadan tam yükleme geri dönme neden olur. Bu ayarı ekleme, yalnızca delta değişiklikler geri yeniden çalışma sırasında aktarılmasını sağlar.

## <a name="step-1-create-a-vault"></a>1. adım: bir kasa oluşturma
1. İçinde toohello oturum [Azure portal](https://manage.windowsazure.com/).
2. Genişletme **Veri Hizmetleri** > **kurtarma Hizmetleri** tıklatıp **Site Recovery kasası**.
3. **Yeni Oluştur** > **Hızlı Oluştur**'a tıklayın.
4. İçinde **adı**, bir kolay ad tooidentify hello kasası girin.
5. İçinde **bölge**, hello hello kasa için coğrafi bölgeyi seçin. desteklenen toocheck bölgeler Bkz [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
6. **Kasa Oluştur**'a tıklayın.
    ![Kasa oluşturma](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Kasa hello onay hello durum çubuğu tooconfirm başarıyla oluşturuldu. Merhaba kasası listelenir **etkin** hello ana üzerinde **kurtarma Hizmetleri** sayfası.

## <a name="step-2-set-up-an-azure-network"></a>2. adım: Bir Azure ağı ayarlama
Azure ağı ayarlama Azure Vm'lerinin yük devretme sonrasında bağlı tooa ağ olacaktır ve içi yeniden çalışma toohello böylece site beklendiği gibi çalışabilir şekilde ayarlayın.

1. Hello Azure portal, seçin **sanal ağ oluştur** hello ağ adı, IP adresi aralığı ve alt ağ adı belirtin.
2. Toodo geri dönme gerekiyorsa, VPN/ExpressRoute toohello ağ ekleyin. VPN/ExpressRoute toohello ağ bile yük devretme sonrasında eklenebilir.

Azure ağlar hakkında daha fazla bilgi için bkz: [sanal ağlara genel bakış](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Geçiş ağların](../azure-resource-manager/resource-group-move-resources.md) kaynak arasında grupları içinde hello aynı abonelik veya abonelikler arasında Site Recovery dağıtmak için kullanılan ağlar için desteklenmez.
>
>

## <a name="step-3-install-hello-vmware-components"></a>3. adım: hello VMware bileşenlerini yükleme
Tooreplicate VMware sanal makineleri istiyorsanız hello yönetim sunucusunda aşağıdaki adımları izleyin:

1. [Karşıdan](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) ve VMware vSphere Powerclı 6.0 yükleyin.
2. Merhaba sunucuyu yeniden başlatın.

## <a name="step-4-download-a-vault-registration-key"></a>4. adım: kasa kayıt anahtarını indirin
1. Merhaba yönetim sunucusundan Azure'da hello Site kurtarma konsolunu açın. Merhaba üzerinde **kurtarma Hizmetleri** hello kasa tooopen hello sayfasında, **Hızlı Başlangıç** sayfası. Merhaba da açabilirsiniz **Hızlı Başlangıç** hello simgesini tıklatarak herhangi bir zamanda sayfası.

    ![Hızlı Başlangıç simgesi](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Merhaba üzerinde **Hızlı Başlangıç** sayfasında, **hazırlama hedef kaynaklar** > **bir kayıt anahtarı indirin**. Merhaba kayıt dosyası otomatik olarak oluşturulur. Oluşturulduktan sonra beş gün boyunca geçerli değil.

## <a name="step-5-install-hello-management-server"></a>5. adım: hello yönetim sunucusu yükleme
> [!TIP]
> Bu URL'leri hello yönetim sunucusundan erişilebilir olduğundan emin olun:
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. Merhaba üzerinde **Hızlı Başlangıç** sayfasında, hello birleşik yükleme dosyası toohello sunucusu yükle.
2. Merhaba yükleme dosyası toostart hello Kur'u **Site Recovery birleşik Kurulumu** Sihirbazı.
3. İçinde **başlamadan önce**seçin **yükleme hello yapılandırma sunucusu ve işlem sunucusu**.

   ![Başlamadan önce](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. İçinde **üçüncü taraf yazılım lisansı**, tıklatın **kabul ediyorum** toodownload ve MySQL yükleme.

    ![Üçüncü taraf yazılım](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. İçinde **kayıt**göz atın ve hello kasadan indirdiğiniz hello kayıt anahtarını seçin.

    ![Kayıt](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. İçinde **Internet ayarlarını**, hello yapılandırma sunucusu üzerinde çalışan hello sağlayıcısı tooAzure Site Recovery hello Internet üzerinden nasıl bağlanacağını belirleyin.

   * Şu anda hello makinede ayarlanır hello proxy ile tooconnect istiyorsanız seçin **var olan ara sunucu ayarlarıyla Bağlan**.
   * Merhaba sağlayıcısı tooconnect doğrudan istiyorsanız seçin **bir proxy sunucu olmadan doğrudan bağlan**.
   * Merhaba mevcut proxy kimlik doğrulaması gerektiriyorsa veya hello sağlayıcı bağlantısı için özel bir ara sunucu toouse istiyorsanız seçin **özel proxy ayarlarıyla Bağlan**.
     * Özel bir ara sunucu kullanırsanız, toospecify başlangıç adresi, bağlantı noktası ve kimlik bilgileri gerekir.
     * Bir proxy sunucu kullanıyorsanız, zaten olarak hello aşağıdaki URL'lere izin:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Güvenlik duvarı](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. İçinde **Önkoşul denetimi**, kurulum onay toomake hello yükleme çalışabildiğinden emin çalıştırılır.

    ![Ön koşullar](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Merhaba hakkında bir uyarı görünürse **genel zaman eşitleme denetimi**, hello bundan hello sistem saati doğrulayın (**tarih ve saat** ayarları) olan hello aynı hello saat dilimi.

     ![Zaman eşitleme sorunu](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. İçinde **MySQL yapılandırma**, yüklenecek toohello MySQL server örneğinde imzalama kimlik bilgileri oluşturun.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. İçinde **ortam ayrıntıları**tooreplicate VMware Vm'lerini oluşturacağız olup olmadığını seçin. Varsa, Kurulum Powerclı 6.0 yüklü olduğunu denetler.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. İçinde **yükleme konumu**burada tooinstall hello ikili dosyaları istediğiniz ve hello önbellek depolamak seçin. En az 5 GB kullanılabilir disk alanı olan bir sürücü seçebilirsiniz, ancak en az 600 GB kullanılabilir disk alanı olan bir önbellek sürücüsü kullanmanızı öneririz.

   ![Yükleme konumu](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. İçinde **Ağ Seçimi**, hangi hello üzerinde yapılandırma sunucusu çoğaltma veri gönderip hello dinleyicisini (ağ bağdaştırıcısı ve SSL bağlantı noktası) belirtin. Merhaba varsayılan değiştirebilirsiniz (9443) bağlantı noktası. Toplama toothis bağlantı noktası 443 numaralı bağlantı noktasını çoğaltma işlemlerini düzenler bir web sunucusu tarafından kullanılır. 443 çoğaltma trafiğini almak için kullanmayın.

    ![Ağ seçimi](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. İçinde **Özet**, hello bilgileri gözden geçirin ve tıklayın **yükleme**. Yükleme tamamlandığında bir parola oluşturulur. Çoğaltmayı etkinleştirmek, bu nedenle onu kopyalayın ve güvenli bir konumda saklayın olduğunda bu anahtar gerekir.

   ![Özet](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Microsoft Azure kurtarma hizmeti Aracısı proxy Hello ayarlanması gerekir.
> Merhaba yüklemesi tamamlandıktan sonra Microsoft Azure kurtarma Hizmetleri Kabuk hello hello Windows Başlat menüsünden başlatın. Açılan hello komut penceresinde komutlar tooset hello proxy sunucusu ayarlarını kümesi aşağıdaki hello çalıştırın.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>Kurulum hello komut satırından çalıştırma
Ayrıca hello birleşik Sihirbazı hello komut satırından aşağıdaki gibi çalıştırabilirsiniz:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

Konumlar:

* /ServerMode: Zorunlu. Merhaba yükleme hello yapılandırma ve işlem sunucular veya hello işlem sunucusu yalnızca (kullanılan tooinstall ek işlem sunucuları) yükleyip yüklemeyeceğini belirtir. Giriş değerleri: CS, PS.
* InstallDrive: zorunlu. Merhaba bileşenlerinin yüklendiği hello klasörü belirtir.
* / MySQLCredFilePath. Zorunlu. Hello yol tooa dosya hello MySQL sunucusu kimlik bilgileri nerede depolanacağını belirtir. Merhaba şablon toocreate hello dosyası alın.
* / VaultCredFilePath. Zorunlu. Merhaba kasa kimlik bilgileri dosyası konumu.
* /EnvType. Zorunlu. Yükleme türü. Değerler: VMware, NonVMware.
* /PSIP ve /CSIP. Zorunlu. Merhaba işlem sunucusu ve yapılandırma sunucusu IP adresi.
* /PassphraseFilePath. Zorunlu. Merhaba parola dosyasının konumu.
* / ByPassProxy. İsteğe bağlı. Ara sunucu olmadan tooAzure bağlayan hello yönetim sunucusunu belirtir.
* /ProxySettingsFilePath. İsteğe bağlı. (Kimlik doğrulaması gerektiren hello sunucusundaki varsayılan proxy) ya da özel proxy özel bir ara sunucu ayarlarını belirtir.

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>6. adım: Merhaba vCenter sunucusu için kimlik bilgilerini ayarlayın
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

Merhaba işlem sunucusu VMware vCenter sunucusu tarafından yönetilen sanal makineleri otomatik olarak bulabilir. Otomatik bulma için Site Recovery bir hesap ve hello vCenter sunucusuna erişmek için kimlik bilgileri gerekir. Bu, yalnızca fiziksel sunucuları çoğaltıyorsanız ilgili değildir.

tooset hello hesabı ve kimlik bilgileri:

1. Merhaba vCenter sunucusunda, bir rol oluşturmak (**Azure_Site_Recovery**) hello vCenter düzeyindeki hello [gerekli izinleri](#vmware-permissions-for-vcenter-access).
2. Merhaba atamak **Azure_Site_Recovery** rol tooa vCenter kullanıcı.

   > [!NOTE]
   > Merhaba salt okunur rolüne sahip bir vCenter kullanıcı hesabı, korumalı kaynak makinelerden kapatmadan yük devretme çalıştırabilirsiniz. Bu makineleri aşağı tooshut istiyorsanız Azure_Site_Recovery rol hello gerekir. Yalnızca VM'ler VMware tooAzure geçiş ve geri toofail olması gerekmez, hello salt okunur rol yeterli olur.
   >
   >
3. tooadd hello hesap, open **cspsconfigtool**. Merhaba Masaüstünde kısayol olarak kullanılabilir ve bulunduğu hello [yükleme konumu] \home\svsystems\bin klasöründe bulunur.
4. Merhaba üzerinde **hesaplarını yönetme** sekmesini tıklatın, **hesabı Ekle**.

    ![Hesap ekleme](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. İçinde **hesap ayrıntıları**, kullanılan tooaccess olabilir kimlik bilgilerini hello vCenter sunucusu ekleyin. Merhaba Portalı'nda, 15 dakikadan fazla hello hesap adı tooappear alabilir. tooupdate hemen tıklatın **yenileme** hello üzerinde **yapılandırma sunucularına** sekmesi.

    ![Ayrıntılar](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>7. adım: vCenter sunucuları ve ESXi konakları ekleme
VMware sanal makinelerini çoğaltıyorsanız tooadd bir vCenter sunucusu (veya ESXi ana bilgisayar) gerekir.

1. Merhaba üzerinde **sunucuları** > **yapılandırma sunucularına** sekmesine **vCenter Sunucusu Ekle**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. Merhaba vCenter sunucusu veya ESXi ana bilgisayar ayrıntıları, hello hello önceki adımda vCenter server ve hello vCenter sunucusu tarafından yönetilen kullanılan toodiscover VMware Vm'lerini olacaktır hello işlem sunucusu tooaccess hello belirtilen hello hesabının adını ekleyin. Merhaba vCenter sunucusu veya ESXi ana bilgisayar aynı ağ üzerinde hangi hello işlem sunucusu yüklü hello sunucusu olarak hello alanında bulunmalıdır.

   > [!NOTE]
   > Merhaba vCenter sunucusu veya ESXi ana hello vCenter veya ana bilgisayar sunucusunda yönetici ayrıcalıklarına sahip olmayan bir hesapla ekliyorsanız hello vCenter veya ESXi hesapları etkin bu ayrıcalıklarına sahip olduğundan emin olun: Datacenter, veri deposu, klasör, Jost, ağ, Kaynak, sanal makine ve vSphere dağıtılmış anahtar. Merhaba vCenter sunucusu hello depolama ayrıcalık etkinleştirilmiş görünümlere gerekir.
   >
   >

    ![VCenter server ekleme](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Bulma işlemi tamamlandıktan sonra hello vCenter sunucusu üzerinde hello listelenmez **yapılandırma sunucularına** sekmesi.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>8. adım: bir koruma grubu oluşturma
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Koruma grupları sanal makinelerin mantıksal gruplandırmaları veya aynı koruma ayarlarını kullanarak tooprotect istediğiniz fiziksel sunucuları hello. Koruma ayarlarını tooa koruma grubu uygulanır ve bu ayarları uygulanan tooall (sanal veya fiziksel) makinelerdir toohello grubunu ekleyin.

1. Çok Git**korunan öğeler** > **koruma grubu** ve hello simgesi tooadd bir koruma grubu tıklatın.

    ![Koruma grubu oluşturma](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Merhaba üzerinde **koruma grubu ayarlarını belirtin** sayfasında, hello grubu için bir ad belirtin. Merhaba, **gelen** açılan listesinden, toocreate hello Grup istediğiniz select hello yapılandırma sunucusu. **Hedef** Microsoft Azure.

    ![Koruma grubu ayarları](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Merhaba üzerinde **çoğaltma ayarlarını belirt** sayfasında, hello grubundaki tüm hello makineler için kullanılacak hello çoğaltma ayarlarını yapılandırın.

    ![Koruma grubunun çoğaltma](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Çoklu VM tutarlılığı**: bunu açmanızı, paylaşılan uygulama tutarlı kurtarma noktalarına hello koruma grubundaki hello makinelerde oluşturur. Merhaba koruma grubundaki tüm makineleri çalıştırırken bu ayarı en uygun hello aynı iş yükünü. Tüm makineler kurtarılan toohello olacaktır aynı veri noktası. VMware Vm'lerini veya fiziksel sunucular (Windows veya Linux) çoğaltma yapıyorsanız bu kullanılabilir.
   * **RPO eşiği**: kümeleri hello RPO. Merhaba sürekli veri koruma çoğaltma yapılandırılmış hello RPO eşik değerini aştığında uyarıları üretilir.
   * **Kurtarma noktası bekletme**: hello bekletme penceresi belirtir. Korumalı makineler olabilir tooany noktası bu pencereyi içinde kurtarıldı.
   * **Uygulamayla tutarlı anlık görüntü sıklığı**: uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktalarının ne sıklıkta oluşturulacak belirtir.

Merhaba onay işareti seçtiğinizde, bir koruma grubu, belirtilen hello adıyla oluşturulur. Ayrıca, ikinci bir koruma grubu hello adıyla oluşturulur *koruma grubu adı*- yeniden çalışma. Yük devretme tooAzure sonra geri toohello şirket içi site başarısız olursa bu koruma grubu kullanılır. Merhaba üzerinde oluşturuldukları gibi hello koruma grupları izleyebilirsiniz **korunan öğeler** sayfası.

## <a name="step-9-install-hello-mobility-service"></a>9. adım: hello Mobility hizmetini yükleme
sanal makineler ve fiziksel sunucuları için korumayı etkinleştirme hello ilk adımı tooinstall hello Mobility hizmetidir. Bunu iki şekilde yapabilirsiniz:

* Otomatik olarak yükleyebilir ve gönderebilir hello hizmet hello işlem sunucusundan her makinede. Makineler tooa koruma grubu ekleyin ve bunlar hello Mobility hizmeti uygun bir sürümünü çalıştırıyorsanız, anında yükleme karşılaşılmaz. Merhaba hizmet WSUS veya System Center Configuration Manager gibi Kurumsal gönderme yöntemini kullanarak da otomatik olarak yükleyebilirsiniz. Bunu yapmadan önce hello yönetimi sunucusunu ayarlama ayarladığınızdan emin olun.
* Merhaba hizmet tooprotect istediğiniz her makinede el ile yükleyin. Bunu yapmadan önce hello yönetimi sunucusunu ayarlama ayarladığınızdan emin olun.

### <a name="install-hello-mobility-service-with-push-installation"></a>Gönderme yüklemesi ile Merhaba Mobility hizmetini yükleme
Makineler tooa koruma grubu eklediğinizde, hello Mobility hizmeti otomatik olarak gönderilir ve her makineye hello işlem sunucusu tarafından yüklenmiş.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Windows makinelerinde otomatik gönderim için hazırlanma
Mobility hizmeti hello şekilde tooprepare Windows makineler hello işlem sunucusu tarafından otomatik olarak yüklenebilir:

1. Bu hello işlem sunucusu tooaccess hello makinenin kullanabileceği bir hesap oluşturun. Merhaba hesap (yerel veya etki alanı) yönetici ayrıcalıklarına sahip. Bu kimlik bilgileri yalnızca itme yüklemesi hello Mobility hizmeti için kullanılır.

   > [!NOTE]
   > Bir etki alanı hesabı kullanmıyorsanız toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir. toodo bunu hello defterinde HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System altında hello DWORD girdisi ekleyin LocalAccountTokenFilterPolicy değerinin 1 ile altında. CLI tooadd hello kayıt defteri girdisinden Aç komutunu veya PowerShell kullanarak girin  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Tooprotect istediğiniz hello makine üzerindeki Windows Güvenlik Duvarı için seçin **bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin**ve etkinleştirme **dosya ve Yazıcı Paylaşımı** ve **Windows Yönetimi İzleme**. Tooa etki alanına ait makineler için bir GPO ile Merhaba güvenlik duvarı ilkesi yapılandırabilirsiniz.

   ![Güvenlik duvarı ayarları](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Oluşturduğunuz hello hesabı ekleyin:

   * **Cspsconfigtool**’u açın. Merhaba Masaüstünde kısayol olarak kullanılabilir ve bulunduğu hello [yükleme konumu] \home\svsystems\bin klasöründe bulunur.
   * Merhaba üzerinde **hesaplarını yönetme** sekmesini tıklatın, **hesabı Ekle**.
   * Oluşturduğunuz hello hesabı ekleyin. Merhaba hesabını ekledikten sonra bir makine tooa koruma grubu eklediğinizde tooprovide hello kimlik bilgilerine ihtiyacınız vardır.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Linux sunucularında otomatik gönderim için hazırlanma
1. İstediğiniz tooprotect açıklandığı gibi desteklenen o hello Linux makine emin olun [şirket içi Önkoşullar](#on-premises-prerequisites). Ağ bağlantısı olduğundan emin olun hello makine arasında istediğiniz hello işlem sunucusu çalıştıran tooprotect ve hello yönetim sunucusu.
2. Bu hello işlem sunucusu tooaccess hello makinenin kullanabileceği bir hesap oluşturun. Merhaba hesap kök kullanıcı hello kaynak Linux sunucusu üzerinde olmalıdır. Bu kimlik bilgileri yalnızca itme yüklemesi hello Mobility hizmeti için kullanılır.

   * **Cspsconfigtool**’u açın. Merhaba Masaüstünde kısayol olarak kullanılabilir ve bulunduğu hello [yükleme konumu] \home\svsystems\bin klasöründe bulunur.
   * Merhaba üzerinde **hesaplarını yönetme** sekmesini tıklatın, **hesabı Ekle**.
   * Oluşturduğunuz hello hesabı ekleyin. Merhaba hesabını ekledikten sonra bir makine tooa koruma grubu eklediğinizde tooprovide hello kimlik bilgilerine ihtiyacınız vardır.
3. Tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin girişleri sunucusunu içeren Linux hello kaynağında o hello/etc/hosts dosyasını kontrol edin.
4. Merhaba son openssh, openssh sunuculu ve openssl paketleri tooprotect istediğiniz hello makineye yükleyin.
5. SSH bağlantı noktası 22 etkin ve çalışıyor olduğundan emin olun.
6. SFTP alt sistemi ve parola kimlik doğrulaması hello sshd_config dosyasında aşağıdaki gibi etkinleştirin:

   * Kök olarak oturum açın.
   * Merhaba /etc/ssh/sshd_config dosyasında PasswordAuthentication ile başlayan hello satırını bulun.
   * Merhaba satırı açıklamadan çıkarın ve hello değerinden değiştirme **hiçbir** çok**Evet**.
   * İle başlayan Bul hello satır **alt sistemi** ve hello satırı açıklamadan çıkarın.

     ![Linux hiçbir alt sistemlerin varsayılan geçersiz kılma](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>Merhaba Mobility hizmeti el ile yükleyin
Merhaba yükleyicileri C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository içinde kullanılabilir.

| Kaynak işletim sistemi | Mobility hizmeti yükleme dosyası |
| --- | --- |
| Windows Server (yalnızca 64 bit) |Microsoft-ASR_UA_9*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (yalnızca 64 bit) |Microsoft-ASR_UA_9*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (yalnızca 64 bit) |Microsoft-ASR_UA_9*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (yalnızca 64 bit) |Microsoft-ASR_UA_9*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Merhaba Mobility hizmeti el ile bir Windows sunucusuna yükleyin
1. Karşıdan yükle ve hello ilgili yükleyiciyi çalıştırın.
2. **Başlamadan önce** bölümünde **Mobility hizmeti**’ni seçin.

    ![Mobility hizmeti yüklemesi](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. İçinde **yapılandırma sunucusu ayrıntılarını**hello hello yönetim sunucusunun IP adresi belirtin ve hello yönetim sunucusu bileşeni yüklü olduğunda, oluşturulan parola hello. Çalıştırarak hello parola alabilir  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** hello yönetim sunucusunda.

    ![Mobility hizmeti](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. İçinde **yükleme konumu**, hello varsayılan Konum'u tutabilir ve tıklayın **sonraki** toobegin yükleme.
5. İçinde **yükleme ilerleme durumu**, yükleme kontrol edin ve istenirse hello makineyi yeniden başlatın.

Ayrıca, metin hello komut satırı aşağıdaki hello girerek yükleyebilirsiniz:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

Komut önceki hello:

* / Rol: zorunlu. Merhaba Mobility hizmeti yüklü olup olmadığını belirtir.
* / Installlocation: zorunlu. Burada tooinstall hello hizmet belirtir.
* / PassphraseFilePath: zorunlu. Merhaba yapılandırma sunucusunun parolası belirtir.
* / LogFilePath'i: zorunlu. Merhaba günlük kurulum dosyası konumu belirtir.

#### <a name="uninstall-hello-mobility-service-manually"></a>Merhaba mobilite hizmetini elle kaldırın
Merhaba Mobility hizmeti kullanarak kaldırabilirsiniz **Kaldır veya Değiştir bir program** Denetim Masası'ndaki ya da hello komut satırını kullanarak.

Merhaba komutu toouninstall hello komut satırını kullanarak Mobility hizmeti aşağıdaki gibidir:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>Merhaba hello yönetim sunucusunun IP adresini değiştirme
Merhaba Sihirbazı çalıştırdıktan sonra başlangıç IP adresi hello management server'ın aşağıdaki gibi değiştirebilirsiniz:

1. Merhaba dosya hostconfig.exe (Merhaba masaüstünde bulunur) açın.
2. Merhaba üzerinde **genel** sekmesinde, hello hello yönetim sunucusunun IP adresini değiştirin.

   > [!NOTE]
   > Yalnızca başlangıç IP adresi hello management server'ın değiştirin. Yönetim sunucu iletişimleri için başlangıç bağlantı noktası numarası 443 olmalıdır ve **HTTPS kullan** sol etkinleştirilmesi gerekir. Merhaba parolayı değiştirmeyin.
   >
   >

    ![Yönetim sunucusu IP adresi](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>Linux sunucusu üzerinde Hello Mobility hizmeti el ile yükleyin
1. Merhaba uygun tar arşiv toohello Linux makine tooprotect istediğiniz kopyalayın. Altında Hello tabloya bakın [hello Mobility hizmeti el ile yüklemeniz](#install-the-mobility-service-manually) hangi tar arşiv toodetermine kullanmalıdır.
2. Bir kabuk programı açmak ve çalıştırarak hello daraltılmış tar arşiv tooa yerel yol ayıklayın:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Passphrase.txt adlı bir dosya oluşturun hello yerel dizin toowhich hello tar arşiv Merhaba içeriğine ayıklanır. toodo Bu, kopyalama hello parola C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase gelen hello yönetim sunucusunda ve kaydedin çalıştırarak passphrase.txt  *`echo <passphrase> >passphrase.txt`*  hello Kabuğu'nda.
4. Merhaba Mobility hizmeti, komutu aşağıdaki hello girerek yükleyin:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Hello hello yönetim sunucusunun iç IP adresi belirtin ve 443 numaralı bağlantı noktasını seçili olduğundan emin olun.

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>Merhaba komut satırından Hello Mobility hizmetini yükleme

C:\Program Files (x86) \InMage Systems\private\connection hello yönetim sunucusundaki Hello parolayı kopyalayın ve hello yönetim sunucusunda "passphrase.txt" kaydedin. Ardından hello aşağıdaki komutları çalıştırın. Örneğimizde hello yönetim sunucusu IP adresi 104.40.75.37 ve hello HTTPS bağlantı noktası 443'tür:

tooinstall bir üretim sunucusunda:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

tooinstall hello ana hedef sunucusunda:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>10. adım: bir makine için korumayı etkinleştirin
tooenable koruma, sanal makineleri ve fiziksel sunucuları tooa koruma grubuna ekleyin. Başlamadan önce VMware sanal makineleri koruyorsanız hello aşağıdakilere dikkat edin:

* VMware Vm'lerini her 15 dakikada bulunan ve 15 dakikadan fazla bunları tooappear hello Site kurtarma Portalı'nda sonra bulma sürüyor.
* Ortam değişiklikleri (örneğin, VMware araçları yükleme) hello sanal makinedeki birden çok Site Recovery güncelleştirilmiş 15 dakika toobe de alabilir.
* Merhaba en son bulunan zaman VMware Vm'leri için hello denetleyebilirsiniz **en son kişi** hello üzerinde hello vCenter sunucusu/ESXi ana bilgisayar için alan **yapılandırma sunucularına** sekmesi.
* Bir koruma grubu oluşturduktan sonra bir vCenter sunucusu veya ESXi ana bilgisayar eklerseniz, 15 dakikadan fazla hello Azure Site Recovery portalı toorefresh ve sanal makineleri toobe hello listelenen sürebilir **Ekle makineler tooa koruma grubu**iletişim kutusu.
* Tooproceed hemen istediğiniz ve makineler tooa koruma grubu için zamanlanmış bulma hello beklemeden eklerseniz, hello yapılandırma sunucusu vurgulayın (tıklatın yok) tıklatıp **yenileme**.

Buna ek olarak:

* Böylece, iş yüklerini yansıtma koruma gruplarınızı mimari öneririz. Örneğin, belirli bir uygulama toohello çalışan makineleri ekleyin aynı grubu.
* Makineler tooa koruma grubu eklediğinizde, hello işlem sunucusu otomatik olarak iter ve hello Mobility hizmeti zaten yüklü değilse yüklenir. Merhaba önceki adımda açıklanan şekilde hazırlanmış toohave hello itme mekanizması gerekir.

### <a name="add-machines-tooa-protection-group"></a>Makineler tooa koruma grubuna ekleme

1. Çok Git**korunan öğeler** > **koruma grubu** > **makineler** > **eklemek makineler** .
2. VMware sanal makineleri koruyorsanız **sanal makineleri seçin**sanal makineleri (veya bunlar çalışmakta olduğu hello EXSi konak) yönetme bir vCenter sunucusu seçin ve ardından hello makineleri seçin.

    ![Sanal makineler için korumayı etkinleştir](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. İçinde fiziksel sunucuları koruyorsanız **sanal makineleri seçin**açın hello **eklemek fiziksel makineleri** Sihirbazı'nı ve başlangıç IP adresi ve kolay bir ad sağlayın. Ardından hello işletim sistemi ailesi seçin.

   ![Fiziksel sunucuları için korumayı etkinleştirin](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. İçinde **belirtin hedef kaynaklar**, çoğaltma için kullanmakta olduğunuz hello depolama hesabını seçin ve hello ayarları tüm iş yükleri için kullanılması gereken olup olmadığını seçin. Premium depolama hesapları şu anda desteklenmiyor.

   > [!NOTE]
   > Merhaba kullanılarak oluşturulan taşıma depolama hesapları desteklemiyoruz [Azure portal](../storage/storage-create-storage-account.md) kaynak grupları arasında.                           
   > [Geçiş depolama hesaplarının](../azure-resource-manager/resource-group-move-resources.md) kaynak arasında grupları içinde hello aynı abonelik veya abonelikler arasında Site Recovery dağıtmak için kullanılan depolama hesapları için desteklenmez.
   >
   >

    ![Hedef ayarlarını yapılandırma](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. İçinde **belirtin hesapları**seçin hello hesabına [ayarlanan](#install-the-mobility-service-with-push-installation) toouse otomatik hello mobilite hizmetinin yüklenmesi için.

    ![Hesaplarını belirtin](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Makineler toohello koruma grubu ve toostart ilk çoğaltma için her makine ekleme hello onay işareti toofinish'ı tıklatın.

   > [!NOTE]
   > Yükleme hazırlanmış hello Mobility hizmeti toohello koruma grubuna eklenen sahip makinelerde otomatik olarak yüklenir. Merhaba hizmeti yüklendikten sonra bir koruma işi başlatır ve başarısız olur. Merhaba hatasından sonra dolmadığı her makinede Mobility hizmeti yüklenmiş hello toomanually yeniden başlatma gerekir. Merhaba yeniden başlatma işleminden sonra hello koruma işini yeniden başlar ve ilk çoğaltma gerçekleştirilir.
   >
   >

Merhaba durumunu izleyebilirsiniz **işleri** sayfası.

![Merhaba işleri sayfasında durumunu izleyin](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

Koruma durumunu da izlenebilir içinde **korunan öğeler** > *koruma grubu adı* > **sanal makineleri**. İlk çoğaltma sonlandırıldıktan sonra verileri eşitlenir, durum değişikliklerini çok makine**korumalı**.

![Korumalı öğeleri durumunu izleyin](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>11. adım: Korunan kümesi makine özellikleri
1. Bir makine sahip olduktan sonra bir **korumalı** durumu, yük devretme özelliklerini yapılandırabilirsiniz. Merhaba koruma grubu ayrıntılarını seçin makine ve açık hello hello **yapılandırma** sekmesi.
2. Site Recovery otomatik olarak hello Azure VM özelliklerini önerir ve hello içi ağ ayarlarını algılar.

    ![Sanal makine özelliklerini ayarla](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. Bu ayarları değiştirebilirsiniz:

   * **Azure VM adı**: Bu toohello makine yük devretme sonrasında Azure verilecek hello adıdır. Merhaba adı Azure gereksinimlere uygun olmalıdır.
   * **Azure VM boyutu**: ağ bağdaştırıcılarının sayısını hello dikte hello boyutuna göre hello hedef sanal makine için belirtin. Merhaba boyutları ve bağdaştırıcılar hakkında daha fazla bilgi için bkz: [boyut tabloları](../virtual-machines/linux/sizes.md). Şunlara dikkat edin:

     * Bir sanal makine hello boyutunu değiştirmek ve hello ayarları kaydettiğinizde hello açtığınızda hello ağ bağdaştırıcısı sayısı değişir **yapılandırma** sekmesini hello sonraki saat. Hedef sanal makinelerin ağ bağdaştırıcılarında en az sayıda Hello eşit toohello en az bir kaynak sanal makinedeki ağ bağdaştırıcısı sayısıdır. ağ bağdaştırıcısı Hello sayısı hello hello sanal makine boyutu tarafından belirlenir.
       * Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı daha az olup olmadığını veya bu değere eşit toohello bağdaştırıcı sayısı izin verilen hello hedef makine boyutu için hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
       * Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu için izin verilen hello sayıyı aşarsa maksimum hello hedef boyutu kullanılır.
        Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa ancak tek desteklenen hello hedef boyutu destekliyorsa, hello hedef makine yalnızca bir bağdaştırıcısı olur.
     * Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa, tüm bağdaştırıcıları bağlı toohello olmalıdır aynı Azure ağı.
   * **Azure ağı**: Azure sanal makineleri bağlı tooafter yük devretme olacağını bir Azure ağı belirtmeniz gerekir. Bir belirtmezseniz, hello Azure VM'ler bağlı tooany ağ olmayacaktır. Ayrıca, Azure toohello şirket içi siteden toofailback istiyorsanız toospecify bir Azure ağı gerekir. Yeniden çalışma bir Azure ağı ve bir şirket ağı arasında bir VPN bağlantısı gerektirir.
   * **Azure IP adresi/alt ağı**: her ağ bağdaştırıcısı için Azure VM bağlanmak hello alt toowhich hello seçin. Not Hello ağ bağdaştırıcısı hello kaynak makinenin yapılandırılmış toouse statik bir IP adresi varsa, hello Azure VM için statik bir IP adresi belirtebilirsiniz. Statik bir IP adresi sağlamazsanız, herhangi bir kullanılabilir IP adresi ayrılır. Merhaba hedef IP adresi belirtildi ancak zaten başka bir VM Azure tarafından kullanılıyor, yük devretme başarısız olur. Merhaba ağ bağdaştırıcısı hello kaynak makinenin yapılandırılmış toouse DHCP ise, Azure hello ayarı olarak DHCP sahip olacaksınız.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>12. adım: bir kurtarma planı oluşturma ve yük devretme gerçekleştirme
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

Aynı görev veya hello çalıştırmak hello gerçekleştiren birden çok sanal makine üzerinde başarısız olabilir veya tek bir makine için yük devretme çalıştırabilirsiniz aynı iş yükünü. birden çok üzerinden toofail makineleri hello aynı zaman, eklediğiniz bunları tooa kurtarma planı.

toocreate bir kurtarma planı:

1. Merhaba üzerinde **kurtarma planları** sayfasında, **eklemek kurtarma planı** ve bir kurtarma planı ekleyin. Merhaba plan ayrıntılarını belirtin ve seçin **Azure** hello hedefi olarak.

 ![Kurtarma planı yapılandırın](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. İçinde **sanal makineyi Seç**, bir koruma grubu seçin ve ardından hello Grup tooadd toohello kurtarma planındaki makineleri seçin.

 ![Sanal makineleri ekleyin](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

Merhaba plan toocreate gruplarını ve hangi makineler hello kurtarma planında yük devredildi dizisi hello sırası özelleştirebilirsiniz. Komut dosyaları ve el ile gerçekleştirilen eylemleri için ister de ekleyebilirsiniz. Komut dosyaları el ile veya kullanılarak oluşturulabilir [Azure Automation Runbook](site-recovery-runbook-automation.md). Kurtarma planları özelleştirme hakkında daha fazla bilgi için bkz: [kurtarma planları oluşturabilirsiniz](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Yük devretme gerçekleştirme
Bir yük devretme çalıştırmadan önce:

* Bu hello yönetim sunucusu çalışır ve kullanılabilir olduğundan emin olun. Değilse, yük devretme başarısız olur.
* Planlanmamış bir yük devretme çalıştırırsanız:

  * Mümkün olduğu durumlarda, planlanmamış bir yük devretmeyi çalıştırmadan önce birincil makineleri kapatmanız gerekir. Bu hello çalıştıran her iki hello kaynak ve çoğaltılan makinelerin çalışmamasını garantiler aynı anda. Planlanmamış bir yük devretme çalıştırdığınızda, VMware sanal makinelerini çoğaltıyorsanız Site Recovery hello kaynak makinelerden aşağı tooshut denemelisiniz belirtebilirsiniz. Merhaba hello birincil site durumunu, bağlı olarak bu olabilir veya çalışmayabilir. Fiziksel sunucuları çoğaltma yapıyorsanız Site Recovery bu seçeneği sağlamaz.
  * Planlanmamış bir yük devretme birincil makinelerden veri çoğaltma durur, böylece planlanmamış bir yük devretme başladıktan sonra hiçbir veri değişim aktarılan olmaz.
  * Yük devretme sonrasında tooconnect toohello çoğaltma sanal makinesi Azure istiyorsanız, Uzak Masaüstü Bağlantısı hello yük devretmesi çalıştırmadan önce hello kaynak makinesinde etkinleştirin. Ardından RDP bağlantısı hello güvenlik duvarı aracılığıyla izin verin. Ayrıca, yük devretme sonrasında hello ortak uç noktasını hello Azure sanal makine üzerinde RDP tooallow gerekir. İzleyin [en iyi uygulamalar](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) RDP yük devretme sonrasında çalışır tooensure.

> [!NOTE]
> bir yük devretme tooAzure yaptığınızda tooget hello en iyi performansı elde etmek korumalı hello makinede yüklü hello Azure Aracısı. Yardımcı sorunlarını tanılamak ve bu hello makine önyükleme daha hızlı yardımcı olur. Hello Azure aracı için kullanılabilir [Linux](https://github.com/Azure/WALinuxAgent) ve [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
Bir test yük devretme toosimulate çalıştırmak, yük devretme ve kurtarma işlemleri, üretim ortamınızın etkilemez ve normal çoğaltma olanak tanır yalıtılmış bir ağda normal olarak devam edin. Yük devretme testi initiatd hello kaynağı üzerinde ve birkaç yolla içinde çalıştırın:

* **Bir Azure ağı belirtmeyin**: yük devretme testi ağ olmadan çalıştırırsanız, hello test sanal makineleri başlatın ve doğru Azure'da görünmesi kontrol eder. Sanal makineler, yük devretme sonrasında bağlı tooan Azure ağ olmayacaktır.
* **Bir Azure ağı belirtin**: Bu tür bir yük devretme beklendiği gibi hello tüm çoğaltma ortamının gelir ve ağ belirtilen Azure sanal makineleri bağlı toohello olduğunu denetler.

Yük devretme testi toorun:

1. Merhaba üzerinde **kurtarma planları** sayfasında, seçin hello planı ve tıklatın **yük devretme testi**.

 ![Merhaba planı seçin](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. İçinde **sınama yük devretmesi onaylayın**seçin **hiçbiri** hello yük devretme sınaması için bir Azure ağı toouse istemiyorsanız veya select hello ağ toowhich hello test sanal makineleri yük devretme sonrasında bağlanacağı tooindicate. Merhaba onay işareti toostart hello yük devretme'ı tıklatın.

 ![Bir seçim yapın](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Merhaba yük devretme ilerlemeyi izlemek **işleri** sekmesi.

 ![İlerlemeyi izleme](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Hello yük devretme tamamlandıktan sonra ayrıca olması toosee hello çoğaltma Azure makine görünür **sanal makineleri** hello Azure portal'ın. Tooinitiate bir RDP bağlantı toohello Azure VM istiyorsanız hello VM noktadaki tooopen bağlantı noktası 3389 gerekir.
5. Sonra tamamlanmış, yük devretme ulaştığında hello **tam** aşaması, test tıklatın **tam Test** toofinish. İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin.
6. Tıklatın **hello test yük devretme tamamlandığında** tooautomatically hello test ortamını temizleyin. Bu yapıldıktan sonra hello yük devretme testi gösterecektir bir **tam** durumu. Tüm öğeler ve hello yük devretme testi sırasında otomatik olarak oluşturulan VM'ler silinir. Yük devretme testi iki haftadan fazla sürerse zorla toofinish.

### <a name="run-an-unplanned-failover"></a>Planlanmamış bir yük devretmeyi çalıştırma
Planlanmamış yük devretme Azure'dan başlatılır ve hello birincil site kullanılamıyorsa bile gerçekleştirilebilir.

1. Merhaba üzerinde **kurtarma planları** sayfasında, seçin hello planı ve tıklatın **yük devretme** > **planlanmamış yük devretme**.

 ![Merhaba planı seçin](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. VMware sanal makinelerini çoğaltıyorsanız şirket içi sanal makineleri aşağı tooshut deneyebilirsiniz. Bu en yüksek çaba bir eylemdir ve yük devretme hello çaba veya başarılı olup olmadığını devam eder. İşlemi başarılı değil, hata ayrıntıları hello üzerinde görünür **işleri** altında sekmesinde **planlanmamış yük devretme işleri**.

 ![Şirket içi VM'ler kapatılıyor seçeneği](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Fiziksel sunucuları çoğaltma yapıyorsanız bu seçenek kullanılamaz. Tootry tooshut olanlar aşağı el ile mümkünse ihtiyacınız vardır.
 >
 >

3. İçinde **onaylayın yük devretme**, hello yük devretme yönü (tooAzure) doğrulayın ve toouse hello yük devretme için istediğiniz hello kurtarma noktası seçin. Çoğaltma özelliklerini yapılandırıldığında çoklu VM etkinleştirilirse, toohello en son uygulama veya kilitlenme tutarlı kurtarma noktası kurtarabilirsiniz. Öğesini de seçebilirsiniz **özel kurtarma noktası** toorecover tooan önceki bir nokta. Merhaba onay işareti toostart hello yük devretme'ı tıklatın.

 ![Yük devretme yönü onaylayın](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Merhaba bekleyin planlanmamış yük devretme iş toofinish. Merhaba üzerinde yük devretme işleminin ilerleyişini izleyebilirsiniz **işleri** sekmesi. Planlanmamış yük devretme sırasında bir hata oluşmamasına olsa bile tamamlanıncaya kadar hello kurtarma planı çalıştırır. Ayrıca görebilmeniz gerekir toosee hello çoğaltma Azure makine görünür **sanal makineleri** hello Azure Portalı'nda.

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>Tooreplicated Azure connect yük devretme sonrasında sanal makineler
tooconnect tooreplicated azure'daki sanal makinelerde yük devretme sonrasında, şunlar gerekir:

- Merhaba birincil makinede etkin bir Uzak Masaüstü Bağlantısı.
- Windows Güvenlik Duvarı hello birincil makinede tooallow RDP ayarlayın.
- RDP toohello hello Azure sanal makinesi için ortak uç nokta eklenir.

Bu ayarlama hakkında daha fazla bilgi için bkz: [ASR kullanarak yük devretme sonrasında Uzak Masaüstü bağlantı sorunlarını giderme](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="deploy-additional-process-servers"></a>Ek işlem sunucusu dağıtın
200 kaynak makinelerden ötesinde, dağıtımınızın ölçeğini gerekir ya da 2 TB toplam günlük karmaşıklık oranı aşarsa, ek işlem sunucuları toohandle hello trafik hacmi gerekir. bir ek işlem sunucusu onay hello gereksinimleri tooset [ek işlem sunucuları](#additional-process-servers), ve ardından toohello göre hello işlem sunucusunu ayarlama yönergeleri izleyerek. Merhaba sunucuyu ayarladıktan sonra kaynak makine toouse yapılandırabilirsiniz.

### <a name="set-up-an-additional-process-server"></a>Bir ek işlem sunucusu kurma
Bir ek işlem sunucusu ayarlamadıysanız aşağıdaki gibi ayarlayın:

* Birleşik hello Sihirbazı tooconfigure bir yönetim sunucusu yalnızca işlem sunucusu olarak çalıştırın.
* Yalnızca hello yeni işlem sunucusu kullanarak toomanage veri çoğaltma istiyorsanız, korumalı makinelerinizi toomigrate gerekir.

### <a name="install-hello-process-server"></a>Merhaba işlem sunucusu yükleyin
1. Merhaba üzerinde **Hızlı Başlangıç** sayfasında, Site Recovery bileşen yüklemesi hello hello birleşik yükleme dosyasını indirin. Kur'u yeniden çalıştırın.
2. İçinde **başlamadan önce**seçin **ek işlem sunucuları tooscale dağıtım çıkışı eklemek**.

 ![İşlem sunucusu ekleme](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Ne zaman yaptığınız gibi hello Sihirbazı'nı tamamlayın, [ayarlanan](#step-5-install-the-management-server) hello ilk yönetim sunucusu.
4. İçinde **yapılandırma sunucusu ayrıntılarını**hello hello hello yapılandırma sunucusu yüklediğiniz ilk yönetim sunucusunun IP adresini girin ve hello parola girin. Merhaba parola yoksa çalıştırmak  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** hello özgün yönetim sunucusu tooretrieve üzerinde bu.

 ![Yapılandırma sunucusu ayrıntıları](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Makineler toouse hello yeni işlem sunucusu geçirme
1. Açık **yapılandırma sunucularına** > **Server** > *hello özgün yönetim sunucusu adını*  >   **Sunucu ayrıntıları**.

 ![Sunucu Ayrıntıları](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. Merhaba, **işlem sunucuları** listesinde **işlem sunucusunu Değiştir** toochange istediğiniz sonraki toohello sunucu.

 ![Güncelleştirme hello işlem sunucusu](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Seçin **işlem sunucusunu Değiştir**seçin **hedef işlem sunucusunu**, ve ardından yeni yönetim sunucusu seçin hello. Ardından yeni işlem sunucusu hello select hello sanal makineleri işleyecek. Merhaba bilgi simgesi tooget hello sunucu bilgilerini'ı tıklatın. Görüntülenen toohelp kararları yükleme yaptığınız her seçili sanal makine toohello yeni işlem sunucusu olan tooreplicate gerekli olan hello ortalama alanı. Toohello yeni işlem sunucusu çoğaltma hello onay işareti toostart'ı tıklatın.

 ![Merhaba işlem sunucusunu Değiştir](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>VMware vCenter erişim izinlerini
Merhaba işlem sunucusu, bir vCenter sunucusu üzerinde sanal makineleri otomatik olarak bulabilir. tooperform otomatik bulma, hello vCenter düzeyi tooallow Site Recovery tooaccess hello vCenter sunucusunda toodefine bir rol (Azure_Site_Recovery) gerekir. Yalnızca toomigrate VMware makineleri tooAzure gerekir ve azure'dan toofailback olması gerekmez, yeterli bir salt okunur rolü tanımlayabilirsiniz. Bölümünde açıklandığı gibi Hello izinlerini ayarlama [adım 6: Merhaba vCenter sunucusu için kimlik bilgilerini ayarlama](#step-6-set-up-credentials-for-the-vcenter-server). Hello rol izinleri, aşağıdaki tablonun hello özetlenmiştir:

| **Rol** | **Ayrıntılar** | **İzinler** |
| --- | --- | --- |
| Azure_Site_Recovery rolü |VMware VM bulma |Merhaba v merkezi sunucusu için şu ayrıcalıkları atayın:<br/><br/>Veri deposu: Tahsis alanı, Gözat veri deposu, alt düzey dosya işlemleri, dosya, güncelleştirme sanal makine dosyalarını Kaldır<br/><br/>Ağ: Ağ atama<br/><br/>Kaynak: Ata sanal makine tooresource havuzu, sanal makine Gücü Kapat geçirme, sanal makine gücü açma geçirme<br/><br/>Görevler: görev, güncelleştirme görevi oluşturma<br/><br/>Sanal makine > yapılandırma<br/><br/>Sanal makine > etkileşimde bulunma > yanıt soru, cihaz bağlantısı, yapılandırma CD medyasından, yapılandırma disket ortamı, kapatma, açma, VMware araçları yükleme<br/><br/>Sanal makine > Stok > oluşturun, kayıt, kayıt Sil<br/><br/>Sanal makine > sağlama > izin sanal makine indirme, izin sanal makine dosyaları karşıya yükleme<br/><br/>Sanal makine > anlık görüntüleri > anlık görüntüleri kaldırma |
| vCenter kullanıcı rolü |VMware VM bulma/olmadan yük devretme kaynak VM kapatma |Merhaba v merkezi sunucusu için şu ayrıcalıkları atayın:<br/><br/>Veri Merkezi nesnesi > Propagate tooChild nesnesi, rol = salt okunur <br/><br/>Merhaba kullanıcı hello datacenter düzeyinde atanır ve böylece erişim tooall hello nesneleri hello veri merkezinde sahiptir. Merhaba toorestrict hello erişmek istiyorsanız, Ata **erişim yok** hello rolüyle **toochild yayılması** toohello alt nesneleri (ESX konakları, datastores, sanal makineleri ve ağları). |
| vCenter kullanıcı rolü |Yük devretme ve yeniden çalışma |Merhaba v merkezi sunucusu için şu ayrıcalıkları atayın:<br/><br/>Veri Merkezi nesnesi – Propagate toochild nesnesi, rol Azure_Site_Recovery =<br/><br/>Hello kullanıcı datacenter düzeyinde atanır ve bu nedenle erişim tooall hello nesneleri hello veri merkezinde sahiptir.  Merhaba toorestrict hello erişmek istiyorsanız, Ata ** erişim yok ** hello rolüyle **Propagate toochild nesne** toohello alt nesne (ESX konakları, datastores, sanal makineleri ve ağları). |

## <a name="third-party-software-notices-and-information"></a>Üçüncü taraf yazılım uyarılar ve bilgiler
<!--Do Not Translate or Localize-->

Merhaba yazılımını ve bellenimini çalışır durumda hello Microsoft Ürün veya hizmet dayanır veya hello malzemesini içerir projeleri listelenen (topluca "üçüncü taraf kodu").  Microsoft, hello hello üçüncü taraf kodu değil özgün yazarı.  Hello özgün telif hakkı bildirimi ve lisansı altında Microsoft gibi üçüncü taraf kodu alındı, aşağıda belirtilen ayarlanır.

Bir bölümdeki Hello bilgiler üçüncü taraf bileşenleri hello projelerden aşağıda listelenen kod ilgili olduğu. Bu tür lisansları ve bilgi yalnızca bilgilendirme amacıyla sağlanır.  Bu üçüncü taraf kodu Microsoft yazılım lisans hello Microsoft Ürün veya hizmet koşulları altında Microsoft tarafından relicensed tooyou yapılıyor.  

Bölüm B Hello bilgilerinde kullanılabilir tooyou hello özgün lisans şartları altında Microsoft tarafından kurulan üçüncü taraf kodu bileşenleri ilgili olduğu.

Merhaba tam dosya hello üzerinde bulunan [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft tarafından uygulanır olup olmadığını, belirtilmeyen tüm hakları ayırır rıza ya da aksi takdirde.

## <a name="next-steps"></a>Sonraki adımlar
[Yeniden çalışma hakkında daha fazla bilgi](site-recovery-failback-azure-to-vmware-classic.md) toobring Azure'da çalışan başarısız üzerinden makinelerinizi tooyour şirket içi ortamına geri.
