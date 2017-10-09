---
title: "aaaReplicate VMware Vm'lerini ve fiziksel sunucuları tooAzure (Klasik eski) | Microsoft Docs"
description: "Nasıl tooreplicate VM'ler şirket içi açıklar ve eski bir dağıtımda hello Klasik portalındaki Azure Site RECOVERY'yi kullanarak Windows/Linux fiziksel sunucuları tooAzure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>VMware sanal makineleri ve fiziksel sunucuları tooAzure hello Klasik portal (eski) kullanarak Azure Site Recovery ile çoğaltabilmem
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmware-to-azure.md)
> * [Klasik Portal](site-recovery-vmware-to-azure-classic.md)
> * [Klasik Portal (eski)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Site Recovery tooAzure Hoş Geldiniz! Bu makalede, şirket içi VMware sanal makineleri veya Windows/Linux fiziksel sunucuları tooAzure hello Klasik portalda Azure Site RECOVERY'yi kullanarak çoğaltma için eski bir dağıtımı açıklanmaktadır.

## <a name="overview"></a>Genel Bakış
Kuruluşlar nasıl uygulamaların, iş yüklerinin ve verilerin planlanmış ve Planlanmamış kapalı kalma süresi sırasında çalışır ve kullanılabilir kalmasını belirleyen BCDR stratejisine gereksinim ve toonormal çalışma koşullarına mümkün olan en kısa sürede kurtarın. BCDR stratejinizin işletme verilerini güvende tutması, kurtarılabilir şekilde saklaması ve bir olağanüstü durum sırasında iş yüklerinin sürekli olarak kullanılabilir kalmasını sağlaması gerekir.

Site Recovery, yönetme tarafından şirket içi fiziksel sunucuların ve sanal makineleri toohello buluta (Azure'a) veya tooa ikincil veri merkezine çoğaltma tooyour BCDR stratejinize katkı sağlayan bir Azure hizmetidir. Kesinti birincil konumunuzda meydana toohello ikincil konum tookeep uygulamalar ve iş yüklerini kullanılabilir başarısız. Toonormal işlemleri geri döndüğünde geri tooyour birincil konumu başarısız. [Azure Site Recovery nedir?](site-recovery-overview.md) bölümünden daha fazla bilgi edinebilirsiniz.

> [!WARNING]
> Bu makalede içeren **eski yönergeleri**. Yeni dağıtımlar için kullanmayın. Bunun yerine, [bu yönergeleri izleyin](site-recovery-vmware-to-azure.md) toodeploy Site Recovery hello Azure portal'ın veya [bu yönergeleri kullanmak](site-recovery-vmware-to-azure-classic.md) tooconfigure hello gelişmiş dağıtım hello Klasik Portalı'nda. Bu makalede açıklanan hello yöntemini kullanarak zaten dağıttıktan sonra Gelişmiş toohello dağıtım hello Klasik Portalı'nda geçirmek öneririz.
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>Gelişmiş toohello dağıtım geçirme
Bu bölüm, yalnızca bu makalede hello yönergeleri kullanarak Site Kurtarma zaten dağıttıktan sonra ilgili değildir.

toomigrate mevcut dağıtımınıza gerekir:

1. Şirket içi sitenizdeki yeni Site Recovery bileşenlerini dağıtın.
2. Merhaba yeni yapılandırma sunucusunda VMware vm'lerinin otomatik bulma için kimlik bilgilerini yapılandırın.
3. Merhaba yeni yapılandırma sunucusuyla Hello VMware sunucularını bulur.
4. Merhaba yeni yapılandırma sunucusu ile yeni bir koruma grubu oluşturun.

Başlamadan önce:

* Geçiş için bir bakım penceresi ayarlamanızı öneririz.
* Merhaba **geçirmek makineler** seçenek, yalnızca eski dağıtımı sırasında oluşturulan mevcut koruma gruplarınız varsa kullanılabilir.
* Merhaba geçiş adımlarını tamamladıktan sonra tooa koruma grubuna ekleyebilirsiniz böylece, 15 dakika veya daha uzun toorefresh hello kimlik bilgilerini ve toodiscover ve yenileme sanal makineleri alabilir. Bekleme yerine el ile yenileyebilirsiniz.

Aşağıdaki gibi Geçir:

1. Hakkında bilgi edinin [gelişmiş dağıtım hello Klasik Portalı'nda](site-recovery-vmware-to-azure-classic.md). Gelişmiş gözden geçirme hello [mimarisi](site-recovery-vmware-to-azure-classic.md), ve [Önkoşullar](site-recovery-vmware-to-azure-classic.md).
2. Şu anda çoğaltma yapıyorsanız makinelerden Hello mobilite hizmetini kaldırın. Toohello yeni koruma grubu eklediğinizde hello hizmetinin yeni bir sürümünü hello makinelere yüklenecek.
3. Karşıdan bir [kasa kayıt anahtarını](site-recovery-vmware-to-azure-classic.md) ve [hello birleşik Kurulum Sihirbazı'nı çalıştırın](site-recovery-vmware-to-azure-classic.md) tooinstall hello yapılandırma sunucusu, işlem sunucusu ve ana hedef sunucusu bileşenleri. Daha fazla bilgi edinin [kapasite planlaması](site-recovery-vmware-to-azure-classic.md).
4. [Kimlik bilgilerini ayarlayın](site-recovery-vmware-to-azure-classic.md) , Site kurtarma tooaccess VMware kullanabilirsiniz sunucu tooautomatically VMware Vm'lerini keşfedin. Hakkında bilgi edinin [gerekli izinleri](site-recovery-vmware-to-azure-classic.md).
5. Ekleme [vCenter sunucuları veya vSphere ana](site-recovery-vmware-to-azure-classic.md). Merhaba Site kurtarma Portalı'nda, sunucuları tooappear için daha fazla bilgi için 15 dakika sürebilir.
6. Oluşturma bir [yeni koruma grubu](site-recovery-vmware-to-azure-classic.md). Böylece Hello sanal makineler bulunan ve görünür hello portal toorefresh too15 dakika yukarı alabilir. Toowait istemiyorsanız hello yönetim sunucusu adı vurgulayın (tıklatın yok) > **yenileme**.
7. Merhaba yeni koruma grubu altında tıklatın **geçirmek makineler**.

    ![Hesap ekleme](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. İçinde **seçin makineler** gelen toomigrate istediğiniz ve hello toomigrate istediğiniz makineleri seçin hello koruma grubu.

    ![Hesap ekleme](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. İçinde **hedef ayarlarını yapılandır** toouse isteyip istememenize bağlı hello tüm makineler ve select hello işlem sunucusu ve Azure depolama hesabı için aynı ayarları. Ayrı bir işlem sunucusu yoksa bu hello hello hello yapılandırma sunucusu IP adresi olacaktır.

    ![Hesap ekleme](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [Geçiş depolama hesaplarının](../resource-group-move-resources.md) kaynak arasında grupları içinde hello aynı abonelik veya abonelikler arasında Site Recovery dağıtmak için kullanılan depolama hesapları için desteklenmez.

1. İçinde **belirtin hesapları**, makine toopush hello yeni sürümünü hello Mobility hizmeti hello işlem sunucusu tooaccess hello için oluşturduğunuz hello hesabını seçin.

   ![Hesap ekleme](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. Site Recovery, sağladığınız çoğaltılan veriler toohello Azure depolama hesabınızın geçirirsiniz. İsteğe bağlı olarak hello eski dağıtımda kullanılan hello depolama hesabını yeniden kullanabilirsiniz.
3. Merhaba işinden sonra biter sanal makineleri otomatik olarak eşitler. Eşitleme tamamlandıktan sonra hello eski koruma grubundan hello sanal makineleri silebilirsiniz.
4. Tüm makineler geçirildikten sonra hello eski koruma grubu silebilirsiniz.
5. Eşitleme tamamlandıktan sonra Azure ağ ayarlarını hello ve makineler toospecify hello yük devretme özelliklerini unutmayın.
6. Var olan kurtarma planları varsa, bunları hello ile geliştirilmiş toohello dağıtımı geçirebilirsiniz **geçirmek Kurtarma planlaması** seçeneği. Tüm korumalı makineler geçirildikten sonra yalnızca bunu yapmanız gerekir.

   ![Hesap ekleme](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> Geçiş bitirdikten sonra hello ile devam [Gelişmiş makale](site-recovery-vmware-to-azure-classic.md). Merhaba, bu eski makalenin kalanında artık ilgili olacaktır ve toofollow herhangi gerekmediğinde açıklanan BT ** hello adımlardan birkaçı.
>
>

## <a name="what-do-i-need"></a>Ne yapmalıyım?
Bu diyagramda hello dağıtım bileşenleri gösterilmektedir.

![Yeni kasa](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

İşte gerekenler:

| **Bileşen** | **Dağıtım** | **Ayrıntılar** |
| --- | --- | --- |
| **Yapılandırma sunucusu** |Bir Azure standart A3 sanal makinede hello Site Recovery aynı abonelik. |Merhaba yapılandırma sunucusu korumalı makineler, hello işlem sunucusu ve Azure ana hedef sunucular arasındaki iletişimi düzenler. Yük devretme oluştuğunda çoğaltma ve Azure koordinatları kurtarma ayarlar. |
| **Ana hedef sunucu** |Bir Azure sanal makinesi — bir Windows Server 2012 R2 galeri görüntüsü (tooprotect Windows makineler) veya Linux sunucusu olarak temel ya da bir Windows server tabanlı bir OpenLogic CentOS 6.6 galeri görüntüsü (tooprotect Linux makineler).<br/><br/> Üç boyutlandırma seçenekleri kullanılabilir – standart A4, standart D14 ve standart DS4.<br/><br/> Merhaba bağlı toohello sunucusudur hello yapılandırma sunucusu olarak aynı Azure ağı.<br/><br/> Merhaba Site Recovery portalında ayarlayın |Alır ve Azure depolama hesabınızdaki blob depolama oluşturulan ekli VHD'lerin korumalı makinelerinizi çoğaltılmış verileri korur.<br/><br/> Standart DS4, özellikle tutarlı yüksek performans ve düşük gecikme süresi Premium depolama hesabı kullanarak gerektiren iş yükleri için koruma yapılandırması için seçin. |
| **İşlem sunucusu** |Windows Server 2012 R2 çalıştıran bir şirket içi sanal veya fiziksel sunucu<br/><br/> Bunu yerleştirilen hello üzerinde aynı öneririz ağ ve LAN kesimi tooprotect istiyor, ancak korunan makinelerin L3 olduğu sürece farklı bir ağda çalıştırabilirsiniz hello makineler olarak ağ görünürlük tooit.<br/><br/> Bunu ayarlamak ve hello Site Recovery portalında toohello yapılandırma sunucusuna kaydedin. |Korumalı makineler çoğaltma verileri toohello şirket içi işlem sunucusuna gönderir. Aldığı bir disk tabanlı önbelleği toocache çoğaltma verileri içeriyor. Bu verilere göre çeşitli eylemleri gerçekleştirir.<br/><br/> Veri önbelleğe alma, sıkıştırma ve toohello ana hedef sunucusunda göndermeden önce şifreleme iyileştirir.<br/><br/> Merhaba mobilite hizmetinin göndermeli yüklemesi işler.<br/><br/> VMware sanal makineleri otomatik olarak bulmayı gerçekleştirir. |
| **Şirket içi makineler** |Şirket içi VMware sanal makineleri veya Windows veya Linux çalıştıran fiziksel sunucuları. |Bir veya daha fazla makine geçerli çoğaltma ayarlarını yapılandırın. Tek bir makinede üzerinden veya daha sık kurtarma planına araya toplamak birden çok makine başarısız olabilir. |
| **Mobility hizmeti** |Her sanal makine ya da fiziksel sunucu üzerinde yüklü tooprotect istiyor<br/><br/> Elle yüklenebilir veya gönderilir ve bir makine için çoğaltma etkinleştirdiğinizde hello işlem sunucusu tarafından otomatik olarak yüklenir. |Merhaba Mobility hizmeti (yeniden eşitleme) ilk çoğaltma sırasında veri toohello işlem sunucusuna gönderir. (Yeniden eşitleme bittikten sonra) hello makinenin korumalı bir durumda olduğundan sonra hello Mobility hizmeti yazma toodisk bellek içi yakalar ve bunları toohello işlem sunucusuna gönderir. Windows Server'lar için Applicationconsistency VSS'yi kullanılarak gerçekleştirilir |
| **Azure Site Recovery kasası** |Bir Azure aboneliği ile Site Recovery kasası oluşturduktan ve sunucuları hello kasaya kaydetmek. |Merhaba kasası düzenler ve veri çoğaltma, yük devretme ve şirket içi site ile Azure arasında kurtarma yönetir. |
| **Çoğaltma mekanizması** |**Merhaba Internet üzerinden**— hello Internet üzerinden SSL/TLS güvenli kanalı kullanılarak korunan şirket içi sunucuları tooAzure Communicates ve çoğaltır verileri. Merhaba varsayılan seçenek budur.<br/><br/> **VPN/ExpressRoute**— bir VPN bağlantısı üzerinden şirket içi sunucular ve Azure arasında Communicates ve çoğaltır veri. Siteden siteye VPN veya Azure ağ ve şirket içi site arasında bir ExpressRoute bağlantı tooset gerekir.<br/><br/> Site Recovery dağıtımı sırasında tooreplicate biçiminizi seçersiniz. Varolan makinelerin çoğaltmasını etkilemeden yapılandırıldıktan sonra hello mekanizması değiştiremezsiniz. |Hiçbiri seçeneğini, tooopen korunan makinelerin tüm gelen ağ bağlantı noktalarını gerektirir. Tüm ağ iletişimi hello şirket içi siteden başlatılır. |

## <a name="capacity-planning"></a>Kapasite planlaması
Merhaba ana alanları tooconsider gerekir:

* **Kaynak ortamı**— VMware altyapı, kaynak makine ayarlarını ve gereksinimleri hello.
* **Bileşen sunucularını**— hello işlem sunucusu, yapılandırma sunucusu ve ana hedef sunucusu

### <a name="considerations-for-hello-source-environment"></a>Merhaba kaynak ortamında değerlendirmeleri
* **Maksimum disk boyutu**— hello geçerli en büyük boyutunu ekli tooa sanal makineye bağlanabilir hello disk 1 TB olan. Bu nedenle hello maksimum çoğaltılabilir kaynak disk de sınırlı too1 TB boyutudur.
* **Kaynak başına en fazla boyut**— tek kaynak makinenin hello en büyük boyut: 31 TB (31 disklerle) ve hello ana hedef sunucusu için sağlanan bir D14 örneği.
* **Ana hedef sunucu başına kaynağı sayısını**— birden çok kaynak makine bir tek ana hedef sunucusu ile korunabilir. Ancak, diskleri çoğaltmak gibi hello hello diskin boyutunu yansıtan VHD Azure blob depolama alanında oluşturulur ve bir veri diski toohello ana hedef sunucusu olarak bağlı olduğundan tek kaynak makine birden çok ana hedef sunucuda korunamaz.  
* **Kaynak başına en fazla günlük değişikliği hızını**— zaman hello dikkate önerilen kabul toobe gereken üç faktöre değişikliği oranı kaynağı başına vardır. Merhaba göre hedef dikkate alınacak noktalar iki IOPS hello hedef diskte hello kaynak üzerinde her işlem için gereklidir. Eski veri okuma ve yazma hello yeni veri hello hedef disk üzerinde gerçekleştirilecek olmasıdır.
  * **Günlük hello işlem sunucusu tarafından desteklenen hızını değiştirmek**— birden çok işlem sunucusu kaynak makinenin yayılamaz. Tek bir işlem sunucusu günlük değişim oranı too1 TB destekleyebilir. Bu nedenle 1 TB hello maksimum günlük veri kaynak makine için desteklenen oranı değiştirmektir.
  * **Merhaba hedef disk tarafından desteklenen en yüksek verimlilik**— kaynak disk başına en fazla karmaşası birden fazla 144 GB/gün (ile 8 K yazma boyutu) olamaz. Merhaba performans ve çeşitli yazma boyutları için hello hedef IOPS hello ana hedef bölümdeki Hello tablosuna bakın. Her kaynak IOP hello hedef diskteki 2 IOPS oluşturduğundan bu numarayı iki ile ayrılmalıdır. Hakkında bilgi edinin [Azure ölçeklenebilirlik ve performans hedefleri](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) hello hedef premium depolama hesapları için yapılandırırken.
  * **Merhaba depolama hesabı tarafından desteklenen en yüksek verimlilik**— bir kaynağı birden çok depolama hesabı yayılamaz. Verilen bir depolama hesabı 20.000 istekleri saniye başına maksimum alır ve her kaynak IOP hello ana hedef sunucusunda 2 IOPS oluşturur, IOPS sayısını hello hello kaynak too10, 000 arasında tutmak öneririz. Hakkında bilgi edinin [Azure ölçeklenebilirlik ve performans hedefleri](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) hello kaynağı premium depolama hesapları için yapılandırırken.

### <a name="considerations-for-component-servers"></a>Bileşen sunucuları için ilgili önemli noktalar
Tablo 1 hello sanal makine boyutlarını hello yapılandırma ve ana hedef sunucular için özetler.

| **Bileşen** | **Dağıtılan Azure örnekleri** | **Çekirdek** | **Bellek** | **Max diskleri** | **Disk boyutu** |
| --- | --- | --- | --- | --- | --- |
| Yapılandırma sunucusu |Standart A3 |4 |7 GB |8 |1023 GB |
| Ana hedef sunucusu |Standart A4 |8 |14 GB |16 |1023 GB |
| Standart D14 |16 |112 GB |32 |1023 GB | |
| Standart DS4 |8 |28 GB |16 |1023 GB | |

**Tablo 1**

#### <a name="process-server-considerations"></a>İşlem sunucusu hususları
Genellikle işlem sunucusu boyutlandırma tüm korunan iş yükleri arasında hello günlük değişikliği oranına bağlıdır.

* Satır içi sıkıştırma ve şifreleme gibi yeterli işlem tooperform görevleri gerekir.
* Merhaba işlem sunucusu disk tabanlı önbelleği kullanır. Önbellek alanı önerilen emin hello yapın ve disk performansını ağ sorununu veya kesinti hello olayda depolanan kullanılabilir toofacilitate hello veri değişiklikleri olan.
* Böylece Hello işlem sunucusu hello veri toohello ana hedef sunucusu tooprovide sürekli veri koruması yükleyebilirsiniz yeterli bant genişliği emin olun.

Tablo 2 hello işlem sunucusu yönergeleri özetini sağlar.

| **Veri değişikliği oranı** | **CPU** | **Bellek** | **Önbellek disk boyutu** | **Önbellek disk işleme** | **Bant genişliği giriş/çıkışı** |
| --- | --- | --- | --- | --- | --- |
| < 300 GB |4 Vcpu (2 yuva * 2.5 GHz @ 2 Çekirdek) |4 GB |600 GB |saniye başına 7 too10 MB |30 MB/sn/21 MB/sn |
| 300 too600 GB |8 Vcpu'lar (2 yuva * @ 2.5 GHz 4 çekirdek) |6 GB |600 GB |saniye başına 11 too15 MB |60 MB/sn/42 MB/sn |
| 600 GB too1 TB |12 Vcpu'lar (2 yuva * 2.5 GHz @ 6 çekirdek) |8 GB |600 GB |saniye başına 16 too20 MB |100 MB/sn/70 MB/sn |
| > 1 TB |Başka bir işlem sunucusu Dağıt | | | | |

**Tablo 2**

Konumlar:

* Giriş indirme bant genişliği (intranet hello kaynak ve işlem sunucusu arasında) ' dir.
* Çıkış karşıya yükleme bant genişliği (Internet hello işlem sunucusu ve ana hedef sunucusu arasındaki) ' dir. Çıkış numaraları ortalama % 30 işlem sunucusu sıkıştırma varsayın.
* Önbelleği için ayrı bir işletim sistemi disk en az 128 GB disk tüm işlem sunucuları için önerilir.
* Önbellek disk verimlilik hello için depolama aşağıdaki değerlendirmesi için kullanıldı: 10 K RPM RAID 10 yapılandırmasında ile 8 SAS sürücüleri.

#### <a name="configuration-server-considerations"></a>Yapılandırma sunucusu hususları
Her yapılandırma sunucusu 3-4 birimlerle too100 kaynak makineleri destekleyebilirsiniz. Dağıtımınızı büyükse, başka bir yapılandırma sunucusu dağıtmak öneririz. Tablo 1 hello varsayılan sanal makine özelliklerini hello yapılandırma sunucusu için bkz.

#### <a name="master-target-server-and-storage-account-considerations"></a>Ana hedef sunucu ve depolama hesabında dikkate alınacak noktalar
Merhaba depolama her bir ana hedef sunucusu için işletim sistemi diski, bekletme birimi ve veri diskleri içerir. Hello bekletme sürücüsü hello Site kurtarma Portalı'nda tanımlanan hello bekletme penceresinin hello süresi için disk değişikliklerini hello günlüğünü tutar.  TooTable 1 için hello ana hedef sunucusunun hello sanal makine özelliklerine bakın. Tablo 3 A4 hello disklerin nasıl kullanıldığını gösterir.

| **Örneği** | **İşletim sistemi diski** | **Bekletme** | **Veri diskleri** |
| --- | --- | --- | --- |
| **Bekletme** |**Veri diskleri** | | |
| Standart A4 |1 disk (1 * 1023 GB) |1 disk (1 * 1023 GB) |15 diskleri (15 * 1023 GB) |
| Standart D14 |1 disk (1 * 1023 GB) |1 disk (1 * 1023 GB) |31 diskleri (15 * 1023 GB) |
| Standart DS4 |1 disk (1 * 1023 GB) |1 disk (1 * 1023 GB) |15 diskleri (15 * 1023 GB) |

**Tablo 3**

Kapasite Hello ana hedef sunucusu için planlama bağlıdır:

* Azure depolama performansı ve sınırlamalar
  * Merhaba sayısının yüksek oranda diskler bir standart katmanı VM için kullanılan, yaklaşık 40 (disk başına 20.000/500 IOPS) tek bir depolama hesabı. Hakkında bilgi edinin [standart depolama hesapları için ölçeklenebilirlik hedefleri](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) ve [premium depolama hesapları](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
* Günlük değişim oranı
* Bekletme birimi depolama.

Şunlara dikkat edin:

* Bir kaynak birden çok depolama hesabı yayılamaz. Bu koruma yapılandırdığınızda seçili toohello depolama hesapları Git toohello veri diski geçerlidir. Depolama hesabı toohello otomatik olarak dağıtılan Hello işletim sistemi ve hello bekletme diskleri genellikle gidin.
* hello saklama depolama biriminin gerekli hello günlük değişim oranı ve saklama gün sayısı hello bağlıdır. ana hedef sunucu başına gerekli bekletme depolama Hello günde kaynağından toplam karmaşıklığa = * bekletme gün sayısı.
* Her bir ana hedef sunucusu yalnızca bir bekletme birimi vardır. Merhaba bekletme birimi hello diskleri ekli toohello ana hedef sunucu arasında paylaşılır. Örneğin:
  * Kaynak makine 5 disklerle ve her disk hello kaynağında 120 IOPS (8 K boyut) oluşturur, bu disk (Merhaba hedef disk kaynağı GÇ başına 2 işlemleri) başına too240 IOPS dönüşür. 240 IOPS hello Azure başına 500 disk IOPS sınırı içinde olduğunu.
  * Merhaba bekletme biriminde bu 120 * 5 = 600 olur IOPS ve bu bottle boynu haline gelebilir. Bu senaryoda, iyi bir stratejisi tooadd daha fazla disk toohello bekletme birimi olmalı ve bu yana bir RAID stripe yapılandırma span. Merhaba IOPS dağıtılır çünkü birden çok sürücüde bu performansı iyileştirir. eklenen sürücüleri toobe Hello sayısıdır toohello saklama biriminin şu şekilde olacaktır:
    * Kaynak ortamından toplam IOPS / 500
    * Toplam karmaşıklığa (sıkıştırılmamış) kaynak ortamından günde / 287 GB. Gün başına bir hedef disk tarafından desteklenen en yüksek verimlilik hello 287 GB'dir. Bu durumda 8 K üç yazma boyutu kabul olduğundan bu ölçüm hello yazma boyutu 8 k faktörle göre değişir. Merhaba yazma boyutu verimlilik 287/2 sonra Örneğin, 4 K ise. Ve ardından hello yazma boyutu 16 K ise verimlilik 287 * 2 olacaktır.
* Merhaba gerekli depolama hesabı sayısı toplam kaynak IOP/10000 =.

## <a name="before-you-start"></a>Başlamadan önce
| **Bileşen** | **Gereksinimleri** | **Ayrıntılar** |
| --- | --- | --- |
| **Azure hesabı** |Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. | |
| **Azure depolama alanı** |Bir Azure depolama hesabı toostore çoğaltılmış verileri gerekir<br/><br/> Herhangi bir hello hesabı olmalıdır bir [standart coğrafi olarak yedekli depolama hesabı](../storage/common/storage-redundancy.md#geo-redundant-storage) veya [Premium depolama hesabı](../storage/common/storage-premium-storage.md).<br/><br/> Buna hello hello Azure Site Recovery hizmeti ile aynı bölgeye gerekir ve hello ile ilişkili aynı abonelik. Merhaba taşıma hello kullanılarak oluşturulan depolama hesaplarının desteklemiyoruz [yeni Azure portalına](../storage/common/storage-create-storage-account.md) kaynak grupları arasında.<br/><br/> Daha fazla okuma toolearn [giriş tooMicrosoft Azure depolama](../storage/common/storage-introduction.md) | |
| **Azure sanal ağı** |Yapılandırma sunucusu ve ana hedef sunucusu hangi hello dağıtılacak bir Azure sanal ağınızın olması gerekir. Hello olmalıdır aynı abonelikte ve bölgede hello Azure Site Recovery kasası. Tooreplicate veri bir ExpressRoute veya VPN bağlantısı hello Azure sanal isterseniz, ağ ExpressRoute bağlantısı veya siteden siteye VPN üzerinden bağlı tooyour şirket içi ağ olmalıdır. | |
| **Azure kaynakları** |Yeterli Azure kaynaklarını toodeploy tüm bileşenlere sahip olduğunuzdan emin olun. Daha fazla okuma [Azure abonelik limitleri](../azure-subscription-service-limits.md). | |
| **Azure sanal makineleri** |Sanal makineleri tooprotect istediğiniz uygun ile [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).<br/><br/> **Disk sayısı**— tek bir korumalı sunucu üzerinde en 31 disklerin desteklenebilir<br/><br/> **Disk boyutları**— bağımsız disk kapasitesinin 1023 GB'tan fazla olması gerekir<br/><br/> **Kümeleme**— kümelenmiş sunucular desteklenmez<br/><br/> **Önyükleme**— Birleşik Genişletilebilir Bellenim Arabirimi (UEFI) / Genişletilebilir Bellenim EFI Önyükleme desteklenmiyor<br/><br/> **Birimleri**— Bitlocker şifrelenmiş birimler desteklenmez<br/><br/> **Sunucu adlarını**— adları, 1 ile 63 karakter arasında (harf, rakam ve kısa çizgi) içermelidir. Merhaba adı bir harf veya sayı ile başlamalı ve bir harf veya sayı ile bitmelidir. Bir makine korunduktan sonra hello Azure adını değiştirebilirsiniz. | |
| **Yapılandırma sunucusu** |Bir Azure Site kurtarma Windows Server 2012 R2 galeri görüntüyü temel alarak standart A3 sanal makine, aboneliğinizde hello yapılandırma sunucusu için oluşturulur. Merhaba ilk örnekte yeni bir bulut hizmeti olarak oluşturulur. Merhaba bağlantı türü hello yapılandırma sunucusu hello bulut hizmeti için ayrılmış bir ortak IP adresi ile oluşturulacak gibi genel Internet seçerseniz.<br/><br/> Merhaba yükleme yolu yalnızca İngilizce karakter olmalıdır. | |
| **Ana hedef sunucu** |Azure sanal makinesi, standart A4, D14 veya DS4.<br/><br/> Merhaba yükleme yolu yalnızca İngilizce karakter olmalıdır. Örneğin hello yolu olmalıdır **/usr/local/ASR** Linux çalıştıran bir ana hedef sunucu için. | |
| **İşlem sunucusu** |Fiziksel veya sanal makine hello en son güncelleştirmeleri ile Windows Server 2012 R2 çalıştıran hello işlem sunucusu dağıtabilirsiniz. C'de yüklemek /.<br/><br/> Merhaba üzerinde hello sunucusu Yerleştir öneririz aynı ağ ve alt ağ olarak hello tooprotect istediğiniz makineler.<br/><br/> VMware vSphere CLI 5.5.0 hello işlem sunucusuna yükleyin. Merhaba VMware vSphere CLI bileşen sipariş toodiscover sanal makinelerde bir vCenter sunucusu veya ESXi ana bilgisayarda çalışan sanal makineler tarafından yönetilen hello işlem sunucusu gereklidir.<br/><br/> Merhaba yükleme yolu yalnızca İngilizce karakter olmalıdır.<br/><br/> ReFS dosya sistemi desteklenmiyor. | |
| **VMware** |VMware vSphere hiper yöneticileri yönetmek bir VMware vCenter sunucusu. VCenter sürüm 5.1 veya 5.5 hello en son güncelleştirmeleri ile çalışmalıdır.<br/><br/> VMware sanal makineleri içeren bir veya daha fazla vSphere hiper tooprotect istiyor. Merhaba hiper yönetici ESX/ESXi sürüm 5.1 veya 5.5 hello en son güncelleştirmeleri ile çalıştırıyor olması gerekir.<br/><br/> VMware sanal makineleri VMware araçları yüklü ve çalışıyor olması gerekir. | |
| **Windows makine** |Korumalı fiziksel sunucularda veya Windows çalışan VMware sanal makineleri çeşitli gereksinimler vardır.<br/><br/> A desteklenen 64-bit işletim sistemi: **Windows Server 2012 R2**, **Windows Server 2012**, veya **Itanium tabanlı sistemler için Windows Server 2008 R2 ile en az SP1**.<br/><br/> Merhaba ana bilgisayar adı, bağlama noktaları, aygıt adı, Windows sistem yolu (ör: C:\Windows) İngilizce yalnızca olmalıdır.<br/><br/> Merhaba işletim sistemi C:\ sürücüsünü yüklenmesi gerekir.<br/><br/> Yalnızca temel diskleri desteklenir. Dinamik diskler desteklenmiyor.<br/><br/> Güvenlik duvarı kuralları korumalı makinelerdeki izin vermelidir bunları tooreach hello yapılandırma ve ana hedef sunucular Azure.p ><p>Tooprovide yönetici hesabı gerekir (Merhaba Windows makinesinde yerel yönetici olması gerekir) toopush hello Mobility hizmeti Windows sunucularına yükleyin. Sağlanan hello hesabı bir etki alanı dışı hesabıysa toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir. toodo bu Ekle hello LocalAccountTokenFilterPolicy DWORD kayıt defteri girdisini HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System altında 1 değerine sahip. CLI tooadd hello kayıt defteri girdisinden cmd veya PowerShell'i açın ve girin  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** . [Daha fazla bilgi edinin](https://msdn.microsoft.com/library/aa826699.aspx) erişim denetimi hakkında.<br/><br/> Uzak Masaüstü'nü Azure tooWindows sanal makinelere bağlanmak isterseniz yük devretme sonrasında, Uzak Masaüstü hello şirket içi makinede etkin olduğundan emin olun. VPN üzerinden bağlanıyorsanız değil, güvenlik duvarı kuralları Uzak Masaüstü bağlantıları hello sağlamalıdır Internet. | |
| **Linux makineler** |Desteklenen 64 bit işletim sistemi: **Centos 6.4, 6.5, 6.6**; **Oracle Enterprise Linux 6.4, hello Red Hat uyumlu çekirdek veya kesilemeyen kurumsal çekirdek sürüm 3 (UEK3) çalıştıran 6.5**, **SUSE Linux Enterprise Server 11 SP3**.<br/><br/> Güvenlik duvarı kuralları korumalı makinelerdeki bunları tooreach hello yapılandırma ve ana hedef sunucular ile Azure izin vermelidir.<br/><br/> / etc/hosts dosyaları korumalı makinelerdeki tüm NIC ile ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin giriş içermelidir <br/><br/> Çalışan Linux tooconnect tooan Azure sanal istiyorsanız makine yük devretme bir Secure Shell (ssh), kullanan istemci emin olduktan sonra bu hello korumalı hello Secure Shell hizmetinin makine toostart sistem önyüklemede otomatik olarak ayarlanır ve güvenlik duvarı kuralları izin veren bir ssh bağlantı tooit.<br/><br/> Hello ana bilgisayar adı, bağlama noktaları, aygıt adları ve Linux sistem yolu ve dosya adları (örneğin/etc /; / usr) İngilizce yalnızca olmalıdır.<br/><br/> Koruma etkin depolama aşağıdaki hello ile şirket içi makineler için:-<br>Dosya sistemi: EXT3, ETX4, ReiserFS, XFS<br>Çok yollu yazılım-aygıtı Eşleyici (çok yollu)<br>Birim Yöneticisi: LVM2<br>HP CCISS denetleyicisi depolama ile fiziksel sunucuları desteklenmez. | |
| **Üçüncü taraf** |Bazı dağıtım bileşenleri bu senaryoda, üçüncü taraf yazılım toofunction üzerinde düzgün bir şekilde bağlıdır. Tam bir listesi için bkz: [üçüncü taraf yazılım uyarılar ve bilgiler](#third-party) | |

### <a name="network-connectivity"></a>Ağ bağlantısı
Şirket içi siteniz arasında ağ bağlantısı yapılandırırken iki seçeneğiniz vardır ve Azure sanal ağ üzerinde hangi hello altyapı bileşenlerini (yapılandırma sunucusu, ana hedef sunucuları) dağıtılan hello. Hangi ağ bağlantısı seçeneği toouse, önce yapılandırma sunucusu dağıtabilirsiniz toodecide gerekir. Bu ayarı hello zaman dağıtım toochoose gerekir. Daha sonra değiştirilemez.

**Internet:** iletişimi ve hello şirket içi sunucuları (işlem sunucusu, korumalı makineler) ve hello Azure altyapı bileşen sunucularını (yapılandırma sunucusu, ana hedef sunucusu) arasında verilerin çoğaltılması gerçekleşir güvenli SSL üzerinden / Şirket içi toohello genel Uç noktalara hello yapılandırma ve ana hedef sunucular bağlantısından TLS. (Merhaba tek özel durum hello hello işlem sunucusu ve şifrelenmemiş olan TCP bağlantı noktası 9080 hello ana hedef sunucusu arasındaki bağlantıdır. Yalnızca denetim toohello çoğaltma protokolü için çoğaltması Kurulum bu bağlantıda değiştirilir ilgili bilgiler.)

![Dağıtım Internet diyagram](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**VPN**: iletişimi ve hello şirket içi sunucuları (işlem sunucusu, korumalı makineler) ve hello Azure altyapı bileşen sunucularını (yapılandırma sunucusu, ana hedef sunucusu) arasında verilerin çoğaltılması bir VPN bağlantısı üzerinden gerçekleşir Şirket içi ağınız ve hello Azure arasında sanal ağ üzerinde hangi hello yapılandırma sunucusu ve ana hedef sunucusu dağıtılır. Şirket içi ağınıza bağlı toohello ExpressRoute bağlantısı veya siteden siteye VPN bağlantısı tarafından Azure sanal ağı olduğundan emin olun.

![VPN dağıtım diyagramı](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>1. adım: bir kasa oluşturma
1. İçinde toohello oturum [Yönetim Portalı](https://portal.azure.com).
2. Genişletme **Veri Hizmetleri** > **kurtarma Hizmetleri** tıklatıp **Site Recovery kasası**.
3. **Yeni Oluştur** > **Hızlı Oluştur**'a tıklayın.
4. İçinde **adı**, bir kolay ad tooidentify hello kasası girin.
5. İçinde **bölge**, hello hello kasa için coğrafi bölgeyi seçin. desteklenen toocheck bölgeler coğrafi kullanılabilirlik kısmına bakın [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/)
6. **Kasa Oluştur**'a tıklayın.

    ![Yeni kasa](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

Kasa hello onay hello durum çubuğu tooconfirm başarıyla oluşturuldu. Merhaba kasası listelenir **etkin** hello ana üzerinde **kurtarma Hizmetleri** sayfası.

## <a name="step-2-deploy-a-configuration-server"></a>2. adım: yapılandırma sunucusu dağıtma
### <a name="configure-server-settings"></a>Sunucu ayarlarını yapılandır
1. Merhaba, **kurtarma Hizmetleri** sayfasında, hello kasa tooopen hello hızlı başlangıç sayfasını tıklatın. Hızlı Başlangıç hello simgesini kullanarak herhangi bir zamanda açık olması.

    ![Hızlı Başlangıç Simgesi](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. Merhaba aşağı açılan listesinde seçin **VMware/fiziksel sunucular ve Azure ile şirket içi site arasında**.
3. İçinde **hazırlama Target(Azure) kaynakları** tıklatın **yapılandırma sunucusunu dağıtma**.

    ![Yapılandırma sunucusu dağıtma](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. İçinde **yeni yapılandırma sunucusu ayrıntılarını** belirtin:

   * Merhaba yapılandırma sunucusu ve kimlik bilgilerini tooconnect tooit için bir ad.
   * Merhaba ağ bağlantı türünü seçin bırakma **genel Internet** veya **VPN**. Bu uygulandıktan sonra bu ayarı değiştiremeyeceğinizi unutmayın.
   * Select hello Azure ağ üzerinde hangi hello sunucusu olmalıdır. Emin VPN yapma kullanıyorsanız hello Azure ağı bağlı tooyour şirket içi ağ beklenen biçimde değil.
   * Merhaba iç IP adresi ve toohello sunucusu atanan alt ağ belirtin. Tüm alt ağdaki ilk dört IP adresleriyle hello Not Azure iç kullanımı için ayrılmıştır. Diğer herhangi bir kullanılabilir IP adresi kullanın.

     ![Yapılandırma sunucusu dağıtma](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. Tıkladığınızda **Tamam** aboneliğinizde hello yapılandırma sunucusu için bir Azure Site kurtarma Windows Server 2012 R2 galeri görüntüyü temel alarak standart bir A3 sanal makine oluşturulur. Merhaba ilk örnekte yeni bir bulut hizmeti olarak oluşturulur. Merhaba Internet hello bulut hizmeti üzerinden tooconnect seçtiyseniz, ayrılmış bir ortak IP adresi ile oluşturulur. Merhaba, ilerleme durumunu izleyebilirsiniz **işleri** sekmesi.

    ![İlerlemeyi izleme](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. Hello yapılandırma sunucusu dağıtılan Not hello ortak IP adresi atanmış tooit hello üzerinde tamamlandıktan sonra Internet üzerinden bağlanıyorsanız, hello **sanal makineleri** hello Azure portal sayfasında. Sonra da hello **uç noktaları** sekmesini Not hello genel HTTPS bağlantı noktası eşlenen tooprivate bağlantı noktası 443'tür. Merhaba yapılandırma sunucusuyla hello ana hedef ve işlem sunucuları kaydettiğinizde, daha sonra bu bilgileri gerekir. Merhaba yapılandırma sunucusu bu uç noktalar ile dağıtılır:

   * HTTPS: Genel bir bağlantı noktası kullanılan toocoordinate bileşen sunucular arasında iletişimidir ve Internet üzerinden Azure hello. Özel bağlantı noktası 443 kullanılan toocoordinate bileşen sunucularını ve Azure arasında VPN üzerinden iletişimidir.
   * Özel: Genel bir bağlantı noktası hello geri dönme aracı iletişimi için kullanılır Internet. Özel bağlantı noktası 9443 VPN üzerinden yeniden çalışma aracı iletişimi için kullanılır.
   * PowerShell: Özel bağlantı noktası 5986
   * Uzak Masaüstü: özel 3389 numaralı bağlantı noktası

   ![VM uç noktaları](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > Verme silin veya yapılandırma sunucusu dağıtımı sırasında oluşturulan tüm uç noktaları hello genel veya özel bağlantı noktası numarasını değiştirin.
   >
   >

Merhaba yapılandırma sunucusu ayrılmış bir IP adresiyle bir otomatik olarak oluşturulan Azure bulut hizmetindeki dağıtılır. Merhaba ayrılmış yapılandırma sunucusunun bulut hizmeti IP adresi hello gerekli tooensure adresidir kalır (Merhaba yapılandırma sunucusu dahil) hello sanal makinelerin hello bulut hizmetinde yeniden başlatmalar arasında aynı hello. Merhaba ayrılmış genel IP adresi toobe el ile ayrılmamış gerekir zaman hello yapılandırma sunucusu kullanımdan alındığından veya ayrılmış kalması. 20 ayrılmış genel IP adresleri abonelik başına varsayılan sınır yoktur. [Daha fazla bilgi edinin](../virtual-network/virtual-networks-reserved-private-ip.md) hakkında ayrılmış IP adresleri.

### <a name="register-hello-configuration-server-in-hello-vault"></a>Merhaba kasasına Hello yapılandırma sunucusuna kaydedin
1. Merhaba, **Hızlı Başlangıç** sayfasında **hazırlama hedef kaynaklar** > **bir kayıt anahtarı indirin**. Merhaba anahtar dosyası otomatik olarak oluşturulur. Oluşturulduktan sonra 5 gün boyunca geçerli değil. Toohello yapılandırma sunucusuna kopyalayın.
2. İçinde **sanal makineleri** hello sanal makineler listesinden seçim hello yapılandırma sunucusu. Açık hello **Pano** sekmesinde **Bağlan**. **Açık** hello indirilen RDP dosyası toolog hello yapılandırma sunucuya Uzak Masaüstü kullanarak. VPN kullanıyorsanız, Uzak Masaüstü Bağlantısı hello şirket içi siteden hello iç IP adresi (Merhaba yapılandırma sunucusu dağıtıldığında, belirttiğiniz hello adresi) kullanın. Merhaba ilk kez oturum açtığınızda hello Azure Site kurtarma yapılandırma sunucusu Kurulum Sihirbazı otomatik olarak çalıştırılır.

    ![Kayıt](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. İçinde **üçüncü taraf yazılım yükleme** tıklatın **kabul ediyorum** toodownload ve MySQL yükleme.

    ![MySQL yükleme](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. İçinde **MySQL sunucu ayrıntıları** kimlik bilgileri toolog hello MySQL server örneği üzerine oluşturun.

    ![MySQL kimlik bilgileri](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. İçinde **Internet ayarlarını** hello yapılandırma sunucusu toohello nasıl bağlanacağını belirleyin Internet. Şunlara dikkat edin:

   * Toouse istiyorsanız hello sağlayıcı yüklemeden önce özel bir ara sunucu, onu ayarlamanız gerekir.
   * Tıkladığınızda **sonraki** bir test toocheck hello proxy bağlantı çalışır.
   * Özel bir ara sunucu kullanıyorsanız veya varsayılan ara sunucunuz kimlik doğrulaması gerektiren hello adresi, bağlantı noktası ve kimlik bilgileri dahil olmak üzere, tooenter hello proxy ayrıntılarını gerekir.
   * Aşağıdaki URL'lere hello hello Ara sunucusu üzerinden erişilebilir olması gerekir:
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * IP adresi varsa, güvenlik duvarı kuralları hello kuralları tooallow iletişimi açıklanan hello yapılandırma sunucusu toohello IP adreslerinden ayarlandığından emin olun [Azure veri merkezi IP aralıkları](https://msdn.microsoft.com/library/azure/dn175718.aspx) ve HTTPS (443) protokolü. Merhaba toouse ve, Batı ABD planlama Azure bölgesi toowhite listesi IP aralıklarını gerekir.

     ![Proxy kayıt](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. İçinde **sağlayıcı hata iletisi yerelleştirme ayarları** hangi dilde hata iletileri tooappear istediğinizi belirtin.

    ![Hata iletisi kayıt](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. İçinde **Azure Site Kurtarma kayıt** Gözat ve toohello sunucu kopyaladığınız select hello anahtar dosyası.

    ![Anahtar dosyası kaydı](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. Merhaba Sihirbazı tamamlama sayfasında Hello bu seçenekleri seçin:

   * Seçin **başlatma hesap yönetimi iletişim** hello Sihirbazı tamamladıktan sonra hesapları Yönet iletişim hello toospecify açması gerekir.
   * Seçin **Cspsconfigtool için Masaüstü simgesi oluşturma** tooadd hello yapılandırma sunucusundaki bir masaüstü kısayolu hello açabileceği **hesaplarını yönetme** toorerun hello gerek kalmadan herhangi bir zamanda iletişim Sihirbazı.

     ![Tam kayıt](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. Tıklatın **son** toocomplete hello Sihirbazı. Bir parola oluşturulur. Tooa güvenli bir konuma kopyalayın. Tooauthenticate gerekir ve hello işlem ve ana hedef sunucusu hello yapılandırma sunucusuna kaydedin. Yapılandırma sunucusu iletişimlerde tooensure kanal bütünlüğü de kullandı. Merhaba parolayı yeniden ancak ardından toore kayıt hello ana hedef ve hello yeni parolayı kullanarak işlem sunucuları gerekir.

    ![Parola](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

Kayıttan sonra hello yapılandırma sunucusu üzerinde hello listelenmez. **yapılandırma sunucularına** hello kasası sayfasında.

### <a name="set-up-and-manage-accounts"></a>Ayarlama ve hesaplarını yönetme
Site Recovery dağıtımı sırasında eylemleri aşağıdaki hello için kimlik bilgilerini ister:

* Bir VMware thatSite kurtarma şekilde otomatik olarak bulma Vm'lerinde vCenter sunucuları veya vSphere ana bilgisayar hesabı.
* Ne zaman Site Recovery üzerlerinde hello mobilite hizmetinin yüklenmesi böylece koruma için makineleri ekleyin.

Merhaba yapılandırma sunucusu kaydınız sonra hello açabilirsiniz **hesaplarını yönetme** iletişim tooadd ve bu eylemleri için kullanılması gereken hesaplarını yönetin. Vardır birkaç yolu toodo bu:

* Kurulum hello yapılandırma sunucusu (cspsconfigtool) için son sayfasında hello hello iletişim için toocreated seçti hello kısayol açın.
* Açık hello iletişim kutusunda yapılandırma sunucusu Kurulumu tamamlayın.

1. İçinde **hesaplarını yönetme** tıklatın **hesabı Ekle**. Ayrıca, değiştirebilir ve var olan hesapları silebilirsiniz.

    ![Hesapları yönetme](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. İçinde **hesap ayrıntıları** bir hesap adı toouse Azure ve kimlik bilgileri (etki alanı/kullanıcı adı) belirtin.

    ![Hesapları yönetme](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Toohello yapılandırma sunucusuna bağlanmak
İki yolu tooconnect toohello yapılandırma sunucusu vardır:

* Bir VPN siteden siteye veya ExpressRoute bağlantısı üzerinden
* Üzerinden internet hello

Şunlara dikkat edin:

* İnternet bağlantısı hello sanal makinenin uç noktalarına hello hello genel sanal IP adresi hello server ile birlikte kullanır.
* Bir VPN bağlantısı hello hello sunucusunun iç IP adresi hello birlikte endpoint özel bağlantı noktalarını kullanır.
* Bir kerelik bir karardır toodecide olup tooconnect (Denetim ve çoğaltma verileri), şirket içi sunucuları toohello gelen çeşitli bileşen sunucularını (yapılandırma sunucusu, ana hedef sunucusu) bir VPN bağlantısı üzerinden Azure'da çalışan veya Internet hello. Bu ayarı daha sonra değiştiremezsiniz. Bunu yaparsanız tooredeploy hello senaryo ve makinelerinizi yeniden koruyun.  

## <a name="step-3-deploy-hello-master-target-server"></a>Adım 3: hello ana hedef sunucusu dağıtma
1. Tıklatın **hazırlama Target(Azure) kaynakları** > **ana hedef sunucusu dağıtma**.
2. Merhaba ana hedef sunucu ayrıntıları ve kimlik bilgilerini belirtin. Merhaba sunucu hello dağıtılacak hello yapılandırma sunucusu olarak aynı Azure ağı. Toocomplete tıkladığınızda bir Azure sanal makinesi bir Windows veya Linux galeri görüntüsü ile oluşturulur.

    ![Hedef sunucu ayarları](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

Tüm alt ağdaki ilk dört IP adresleriyle hello Not Azure iç kullanımı için ayrılmıştır. Diğer herhangi bir kullanılabilir IP adresi belirtin.

> [!NOTE]
> Standart DS4 tutarlı yüksek g/ç performans ve düşük gecikme süresi kullanarak sipariş toohost g/ç yoğun iş yükleri de gerektiren iş yükleri için koruma yapılandırırken seçin [Premium depolama hesabı](../storage/common/storage-premium-storage.md).
>
>

1. Bir Windows ana hedef sunucusu VM Bu uç noktalar ile oluşturulur. Yalnızca Internet üzerinden bağlanan Merhaba, ortak uç noktaları oluşturulduğuna dikkat edin.

   * Özel: Merhaba hello işlem sunucusu toosend çoğaltma verileri için kullanılan genel bağlantı noktası Internet. Özel bağlantı noktası 9443 VPN üzerinden hello işlem sunucusu toosend çoğaltma verileri toohello ana hedef sunucusu tarafından kullanılır.
   * Custom1: Merhaba hello işlem sunucusu toosend meta verileri tarafından kullanılan genel bağlantı noktası Internet. Özel bağlantı noktası 9080 VPN üzerinden hello işlem sunucusu toosend meta veri toohello ana hedef sunucusu tarafından kullanılır.
   * PowerShell: Özel bağlantı noktası 5986
   * Uzak Masaüstü: özel 3389 numaralı bağlantı noktası
2. Bir Linux ana hedef sunucusu VM Bu uç noktalar ile oluşturulur. Ortak uç noktalar yalnızca hello bağlanıyorsanız oluşturulduğuna dikkat edin Internet.

   * Özel: Merhaba işlem sunucusu toosend çoğaltma verileri tarafından kullanılan genel bağlantı noktası Internet. Özel bağlantı noktası 9443 VPN üzerinden hello işlem sunucusu toosend çoğaltma verileri toohello ana hedef sunucusu tarafından kullanılır.
   * Custom1: Genel bağlantı noktası hello tarafından hello işlem sunucusu toosend meta veriler kullanılır Internet. Özel bağlantı noktası 9080 VPN üzerinden hello işlem sunucusu toosend meta veri toohello ana hedef sunucusu tarafından kullanılır
   * SSH: Özel bağlantı noktası 22

     > [!WARNING]
     > Verme silin veya herhangi bir hello ana hedef sunucusu dağıtımı sırasında oluşturulan hello uç noktaları hello genel veya özel bağlantı noktası numarasını değiştirin.
     >
     >
3. İçinde **sanal makineleri** hello sanal makine toostart için bekleyin.

   * Bir Windows server Not hello Uzak Masaüstü Ayrıntıları olması durumunda.
   * Linux sunucusudur ve VPN Not hello iç IP adresi hello sanal makinenin bağlandığınız istiyorsanız. Merhaba Internet Not hello genel IP adresi bağlanıyorsanız.
4. Merhaba sunucu toocomplete yüklemeyi oturum ve hello yapılandırma sunucusuna kaydedin.
5. Windows çalıştırıyorsanız:

   1. Bir Uzak Masaüstü Bağlantısı toohello sanal makineyi başlatın. Merhaba, oturum açma komut dosyası ilk kez bir PowerShell penceresinde çalışır. Kapatmayın. Tamamlandığında hello konak Aracısı Yapılandırma Aracı tooregister hello sunucu otomatik olarak açılır.
   2. İçinde **konak Aracısı Yapılandırma** hello iç IP adresi hello yapılandırma sunucusu ve 443 numaralı bağlantı noktasını belirtin. Merhaba sanal makine ekli toohello olduğundan, VPN üzerinden değil bile bağlanıyorsanız hello iç adresi ve özel bağlantı noktası 443 kullanabilirsiniz hello yapılandırma sunucusu olarak aynı Azure ağı. Bırakın **HTTPS kullan** etkin. Daha önce not ettiğiniz hello yapılandırma sunucusu Hello parola girin. Tıklatın **Tamam** tooregister hello sunucu. Merhaba NAT seçenekleri yoksayabilirsiniz. Kullanıldıklarından değil.
   3. Tahmini bekletme sürücü gereksinimi birden fazla 1 TB ise sanal diski kullanarak hello saklama birimi (R:) yapılandırabilirsiniz ve [depolama alanları](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![Windows ana hedef sunucusu](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. Linux çalıştırıyorsanız:

   1. Merhaba hello ana hedef sunucusunu yüklemeden önce en son Linux Tümleştirme hizmetleri (LIS) yüklü olduğundan emin olun yüklediğiniz. Merhaba en son sürümünü LIS yönergeleri birlikte nasıl bulabilirsiniz tooinstall [burada](https://www.microsoft.com/download/details.aspx?id=46842). Merhaba LIS yükledikten sonra hello makineyi yeniden başlatın.
   2. İçinde **hazırlama hedef (Azure) kaynakları** tıklatın **yükleyip ek yazılım (yalnızca Linux ana hedef sunucu için)**. Kopya hello sftp istemci kullanarak tar dosya toohello sanal makine indirilir. Alternatif olarak toohello dağıtılan linux ana hedef sunucuda oturum açın ve kullanmak *wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* toodownload hello hello dosya.
   3. Secure Shell istemcisi kullanarak toohello sunucuda oturum açın. Bağlı değilseniz, toohello Azure ağ VPN üzerinden hello iç IP adresi kullanın. Aksi halde hello dış IP adresi ve hello SSH ortak uç nokta kullanın.
   4. Çalıştırarak hello gzip'li yükleyicisinden Hello dosyaları ayıklayın: **– xvzf Microsoft hedef-ASR_UA_8.4.0.0_RHEL6-64***
      ![Linux ana hedef sunucusu](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. Merhaba dizin toowhich olduğunuzdan emin olun hello hello tar dosyasının içeriğini ayıkladığınız.
   6. Merhaba komutunu kullanarak hello yapılandırma sunucusu parola tooa yerel dosya Kopyala **echo  *`<passphrase>`*  > passphrase.txt**
   7. Hello komutu çalıştır "**sudo. / -t yüklemesi hem - a -R konak MasterTarget -d /usr/local/ASR -i  *`<Configuration server internal IP address>`*  -p 443 -s y - c https -P passphrase.txt**".

      ![Hedef sunucu kaydetme](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. (10-15) birkaç dakika bekleyin ve hello sayfası denetimi hello ana hedef sunucu kayıtlı olarak listelenen **sunucuları** > **yapılandırma sunucularına** **sunucu ayrıntıları** sekmesi. Linux çalıştırıyorsanız ve onu kaydetmedi hello ana bilgisayar yapılandırma aracı /usr/local/ASR/Vx/bin/hostconfigcli yeniden çalıştırın. Kök olarak chmod çalıştırarak tooset erişim izinleri gerekir.

    ![Hedef sunucu doğrulayın](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> Bu, too15 hello Portalı'nda listelenen hello ana hedef sunucusu toobe için kayıt tamamlandıktan sonra dakika sürebilir. tooupdate hemen tıklatın **yenileme** hello üzerinde **yapılandırma sunucularına** sayfası.
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>Adım 4: hello şirket içi işlem sunucusu dağıtma
Başlamadan önce toobe kalıcı çapraz yeniden garanti böylece statik bir IP adresi hello işlem sunucusunda yapılandırmanızı öneririz.

1. Hızlı Başlat'ı > **yükleme işlem sunucusu şirket içi** > **hello işlem sunucusu yükleyip**.

    ![İşlem sunucusu yükleyin](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. Kopya hello zip dosyası toohello sunucu üzerinde tooinstall hello işlem sunucusu oluşturacağız indirilir. Merhaba zip dosyası iki yükleme dosyaları içerir:

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. Merhaba Arşiv ve kopyalama hello yükleme dosyaları tooa konumu hello sunucuda sıkıştırmasını açın.
4. Merhaba çalıştırmak **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** yükleme dosyasını ve izleme hello yönergeler. Bu hello dağıtım için gerekli üçüncü taraf bileşenleri yükler.
5. Ardından çalıştırın **Microsoft-ASR_CX_8.4.0.0_Windows***.
6. Merhaba üzerinde **sunucu modu** sayfasında **işlem sunucusu**.
7. Merhaba üzerinde **ortam ayrıntıları** sayfa hello aşağıdaki:

    - Tooprotect VMware sanal makineleri tıklatın istiyorsanız **Evet**
    - Yalnızca tooprotect fiziksel sunucuları istediğiniz ve böylece VMware vCLI hello işlem sunucusunda yüklü olması gerekmez Tıklatın **Hayır** ve devam edin.

1. VMware vCLI yüklerken Hello aşağıdakileri unutmayın:

   * **Yalnızca VMware vSphere CLI 5.5.0 desteklenir**. Merhaba işlem sunucusu diğer sürümleri veya vSphere CLI güncelleştirmeleri işe yaramaz.
   * VSphere CLI 5.5.0 indirme alanından [burada.](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * VSphere CLI yalnızca hello işlem sunucusu yükleme başlatıldı ve Kurulum onu algılamıyor önce yüklediyseniz, toofive kurulumu tekrar denemeden önce dakika bekleyin. Bu, tüm hello ortam değişkenleri için vSphere CLI algılama düzgün başlatılmadı olduğunu sağlar.
2. İçinde **işlem sunucusu için NIC seçimi** select hello ağ bağdaştırıcısı bu hello işlem sunucusu kullanmalıdır.

   ![Bağdaştırıcıyı seçin](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. İçinde **yapılandırma sunucusu ayrıntılarını**:

   * VPN üzerinden bağlanıyorsanız, başlangıç IP adresi ve bağlantı noktası için hello hello yapılandırma sunucusunun iç IP adresi ve başlangıç bağlantı noktası 443 belirtin. Aksi takdirde hello genel sanal IP adresi ve eşleşen ortak HTTP uç noktası belirtin.
   * Merhaba yapılandırma sunucusunun Hello parola yazın.
   * Clear **doğrulayın Mobility hizmeti yazılım imza** otomatik gönderme tooinstall hello hizmeti kullandığınızda toodisable doğrulama istiyorsanız. İmza doğrulaması hello işlem sunucusundan internet bağlantısı gerekir.
   * **İleri**’ye tıklayın.

   ![Yapılandırma sunucusu kaydetme](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. İçinde **yükleme sürücüsü seçin** bir önbellek sürücüsü seçin. en az 600 GB boş alana sahip bir önbellek sürücüsü Hello işlem sunucusu gerekir. Ardından **Yükle**'ye tıklayın.

   ![Yapılandırma sunucusu kaydetme](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. Not toorestart hello sunucu toocomplete hello yüklemesi gerekebilir. İçinde **yapılandırma sunucusu** > **sunucu ayrıntıları** bu hello işlem sunucusu görünür ve hello kasasına başarıyla kaydedildi denetleyin.

> [!NOTE]
> Yukarı hello yapılandırma sunucusu altında listelendiği gibi hello işlem sunucusu tooappear için kayıt tamamlandıktan sonra too15 dakika sürebilir. tooupdate hemen hello yapılandırma sunucusu sayfa hello altındaki hello yenile düğmesine tıklayarak hello yapılandırma sunucusu Yenile
>
>

![İşlem sunucusu doğrula](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

Merhaba işlem sunucusu kaydolurken hello Mobility hizmeti için imza doğrulamasını devre dışı alamadık, aşağıdaki gibi daha sonra yapabilirsiniz:

1. Merhaba işlem sunucusunda yönetici olarak oturum ve düzenleme C:\pushinstallsvc\pushinstaller.conf hello dosyasını açın. Merhaba bölümünde **[PushInstaller.transport]** bu satırı ekleyin: **SignatureVerificationChecks = "0"**. Merhaba dosyasını kaydedip kapatın.
2. Merhaba Inmage Pushınstall hizmeti yeniden başlatın.

## <a name="step-5-update-site-recovery-components"></a>5. adım: Güncelleştirme Site Recovery bileşenleri
Site Recovery bileşenleri zaman tootime güncelleştirilir. Yeni güncelleştirmeler kullanılabilir olduğunda sırasının hello yüklemeniz gerekir:

1. Yapılandırma sunucusu
2. İşlem sunucusu
3. Ana hedef sunucusu
4. Yeniden çalışma Aracı (vContinuum)

### <a name="obtain-and-install-hello-updates"></a>Alıp hello güncelleştirmelerini yükleyin
1. Site Recovery hello hello yapılandırma, işlem ve ana hedef sunucular için güncelleştirmeleri elde edebilir **Pano**. Linux yüklemesi için hello gzip'li yükleyicisinden hello dosyaları ayıklayın ve hello komutu çalıştır "sudo. / yüklemesi" tooinstall hello güncelleştirme.
2. [Karşıdan](http://go.microsoft.com/fwlink/?LinkID=533813) hello geri dönme tool(vContinuum) için son güncelleştirmeyi hello.
3. Sanal makineleri veya hello Mobility hizmeti zaten yüklü fiziksel sunucuları çalıştırıyorsanız, güncelleştirmelerinin hello hizmeti için aşağıdaki gibi alabilirsiniz:

   * **Seçenek 1**: güncelleştirmelerini yükleme:
     * [Windows Server (yalnızca 64 bit)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4,6.5,6.6 (yalnızca 64 bit)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle Enterprise Linux 6.4,6.5 (yalnızca 64 bit)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server SP3 (yalnızca 64 bit)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Merhaba işlem sunucusu hello güncelleştirdikten sonra hello Mobility hizmeti güncelleştirilmiş sürümünü hello işlem sunucusu hello C:\pushinstallsvc\repository klasöründe kullanılabilir.
   * **Seçenek 2**: hello Mobility hizmeti yüklenmiş daha eski bir sürümüne sahip bir makine varsa, hello hello makinedeki Mobility hizmeti hello Yönetim Portalı'ndan otomatik olarak yükseltebilirsiniz.

     1. Bu hello işlem sunucusu güncelleştirilmiş emin olun.
     2. Bu hello korumalı makine hello ile uyumlu olduğundan emin olun [Önkoşullar](#install-the-mobility-service-automatically) hello güncelleştirme beklendiği gibi çalıştığını bir hello Mobility hizmeti, otomatik olarak gönderilmesi için.
     3. Select hello koruma grubu, Vurgu hello korumalı makine ve tıklatın **güncelleştirme Mobility hizmeti**. Bu düğme, yalnızca hello Mobility hizmetinin daha yeni bir sürümü varsa kullanılabilir.

         ![VCenter sunucusu seçin](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

Select hesaplarında hello korumalı sunucudaki hello yönetici hesabı kullanılan toobe tooupdate hello mobility hizmeti belirtin. Tamam'ı tıklatın ve tetiklenen hello iş toocomplete için bekleyin.

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>Adım 6: vCenter sunucuları veya vSphere ana bilgisayarlar ekleme
1. Tıklatın **sunucuları** > **yapılandırma sunucularına** > yapılandırma sunucusu >**vCenter sunucusu eklemeli** tooadd bir vCenter sunucusu veya vSphere ana bilgisayar.

    ![VCenter sunucusu seçin](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. Merhaba sunucu veya ana bilgisayar ile kullanılan toodiscover olacaktır select hello işlem sunucusu için ayrıntıları belirtin.

   * Merhaba vCenter sunucusu hello varsayılan 443 bağlantı noktasında çalışmıyorsa üzerinde hangi hello vCenter server'ı çalıştıran hello bağlantı noktası numarasını belirtin.
   * Merhaba işlem sunucusu üzerinde aynı hello vCenter sunucusu/vSphere sunucusu ağ ve VMware vSphere CLI 5.5.0 yüklü olmalıdır hello olması gerekir.

     ![vCenter sunucusu ayarları](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. Bulma tamamlandıktan sonra hello vCenter sunucusu hello yapılandırma sunucusu Ayrıntılar altında listelenir.

    ![vCenter sunucusu ayarları](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. Bir yönetici olmayan hesap tooadd hello sunucusu veya ana bilgisayar kullanıyorsanız, hello hesabın ayrıcalıkları aşağıdaki hello olduğundan emin olun:

   * vCenter hesapları Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, depolama görünümleri, sanal makine ve etkin vSphere dağıtılmış anahtar ayrıcalıkları olması gerekir.
   * vSphere ana bilgisayar hesapları hello Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine ve etkin vSphere dağıtılmış anahtar ayrıcalıklarına sahip olmalıdır

## <a name="step-7-create-a-protection-group"></a>7. adım: bir koruma grubu oluşturma
1. Açık **korunan öğeler** > **koruma grubu** > **koruma grubu oluşturma**.

    ![Koruma grubu oluşturma](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. Merhaba üzerinde **koruma grubu ayarlarını belirtin** sayfasında hello grubu ve toocreate hello Grup istediğiniz select hello yapılandırma sunucusu için bir ad belirtin.

    ![Koruma grubu ayarları](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. Merhaba üzerinde **çoğaltma ayarlarını belirt** sayfasında hello grubundaki tüm hello makineler için kullanılacak hello çoğaltma ayarlarını yapılandırın.

    ![Koruma grubunun çoğaltma](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. Ayarlar:

   * **Çoklu VM tutarlılığı**: bunu açmanızı, paylaşılan uygulama tutarlı kurtarma noktalarına hello koruma grubundaki hello makinelerde oluşturur. Tüm hello makineler hello koruma grubundaki çalıştırırken bu ayarı en uygun hello aynı iş yükünü. Tüm makineler kurtarılan toohello olacaktır aynı veri noktası. Yalnızca, Windows sunucuları için de kullanılabilir.
   * **RPO eşiği**: hello sürekli veri koruma çoğaltma RPO'su yapılandırılmış hello RPO eşik değerini aştığında uyarılar oluşturulacak.
   * **Kurtarma noktası bekletme**: hello bekletme penceresi belirtir. Korumalı makineler olabilir tooany noktası bu pencereyi içinde kurtarıldı.
   * **Uygulamayla tutarlı anlık görüntü sıklığı**: uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktalarının ne sıklıkta oluşturulacak belirtir.

Merhaba üzerinde oluşturuldukları gibi hello koruma grubunu izleyebilirsiniz **korunan öğeler** sayfası.

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>8. adım: makineleri ayarlamanız tooprotect istiyor
Tooinstall hello Mobility hizmeti sanal makineleri ve fiziksel sunucularda tooprotect istediğiniz gerekir. Bunu iki şekilde yapabilirsiniz:

* Otomatik olarak yükleyebilir ve gönderebilir hello hizmet hello işlem sunucusundan her makinede.
* Merhaba hizmetini el ile yükleyin.

### <a name="install-hello-mobility-service-automatically"></a>Merhaba Mobility hizmetini otomatik olarak yükleme
Eklerken makineler tooa koruma grubu hello Mobility hizmeti otomatik olarak gönderilir ve hello işlem sunucusu tarafından her makinede yüklü.

**Otomatik olarak yükleme hello mobility hizmeti Windows sunucularında:**

1. Bölümünde açıklandığı gibi hello işlem sunucusu Hello en son güncelleştirmeleri yüklemeniz [adım 5: en son güncelleştirmeleri yükle](#step-5-install-latest-updates)ve bu hello işlem sunucusu kullanılabilir olduğundan emin olun.
2. Merhaba kaynak makine arasında ağ bağlantısı olduğunu ve hello işlem sunucusu ve o hello kaynak makine hello işlem sunucusundan erişilebilir durumda emin olun.  
3. Merhaba Windows Güvenlik Duvarı tooallow yapılandırma **dosya ve Yazıcı Paylaşımı** ve **Windows Yönetim Araçları**. Windows Güvenlik Duvarı ayarları altında "Veya özelliğin güvenlik duvarı aracılığıyla izin ver uygulama" Merhaba seçeneğini ve hello resimde gösterildiği gibi hello uygulamaları seçin. Bir GPO ile Merhaba güvenlik duvarı ilkesini yapılandırabilirsiniz tooa etki alanına ait makineler.

    ![Güvenlik duvarı ayarları](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. Merhaba kullanılan hesap tooperform hello anında yükleme tooprotect istediğiniz hello makinede hello Yöneticiler grubunda olmalıdır. Bu kimlik bilgileri yalnızca hello mobilite hizmetinin göndermeli yüklemesi için kullanılır ve bir makine tooa koruma grubu eklediğinizde sağlarız.
5. Merhaba hesabı bir etki alanı hesabı değilse sağladıysanız toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir. toodo bu Ekle hello LocalAccountTokenFilterPolicy DWORD kayıt defteri girdisini HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System altında 1 değerine sahip. CLI tooadd hello kayıt defteri girdisinden cmd veya PowerShell'i açın ve girin  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .

**Otomatik olarak yükleme hello mobility hizmeti Linux sunucularda:**

1. Bölümünde açıklandığı gibi hello işlem sunucusu Hello en son güncelleştirmeleri yüklemeniz [adım 5: en son güncelleştirmeleri yükle](#step-5-install-latest-updates)ve bu hello işlem sunucusu kullanılabilir olduğundan emin olun.
2. Merhaba kaynak makine arasında ağ bağlantısı olduğunu ve hello işlem sunucusu ve o hello kaynak makine hello işlem sunucusundan erişilebilir durumda emin olun.  
3. Kök kullanıcı hello kaynak Linux sunucuda Hello hesabı olduğundan emin olun.
4. Bu hello/etc/hosts dosyasını hello kaynak sunucu ile tüm NIC ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin girdiler içeriyor Linux emin olun.
5. Merhaba son openssh, openssh-sunucu, openssl paketlerini yüklemek hello makinede tooprotect istiyor.
6. SSH’nin etkin olduğundan ve bağlantı noktası 22’de çalıştırıldığından emin olun.
7. SFTP alt sistemi ve parola kimlik doğrulaması hello sshd_config dosyasında aşağıdaki gibi etkinleştirin:

   * bir) kök olarak oturum açın.
   * b) içinde dosya/etc/ssh hello/hello satır Bul sshd_config dosya başlıyorsa **PasswordAuthentication**.
   * c) hello satırı açıklamadan çıkarın ve "Hayır" Merhaba değerinden çok "Evet" olarak değiştirin.

       ![Linux mobility](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * d) alt sistemi ile başlayan ve hello satırı açıklamadan kaldırmasına Bul başlangıç satırı.

       ![Linux itme mobility](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. Merhaba kaynak makine Linux değişken desteklenen olduğundan emin olun.

### <a name="install-hello-mobility-service-manually"></a>Merhaba Mobility hizmeti el ile yükleyin
Merhaba yazılım paketleri tooinstall hello Mobility hizmeti olan hello işlem sunucusunda C:\pushinstallsvc\repository kullanılır. Merhaba işlem sunucusu ve kopyalama hello uygun yükleme paketini toohello kaynak makine aşağıdaki hello tabloyu temel alan oturum:-

| Kaynak işletim sistemi | İşlem sunucusundaki Mobility hizmet paketi |
| --- | --- |
| Windows Server (yalnızca 64 bit) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4, 6.5, 6.6 (yalnızca 64 bit) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3 (yalnızca 64 bit) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4, 6.5 (yalnızca 64 bit) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**tooinstall hello Mobility hizmeti el ile bir Windows server**, aşağıdaki hello:

1. Kopya hello **Microsoft ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe** Merhaba tablonun toohello kaynak makine üzerinde hello işlem sunucusu dizin yolu paketinden listelenmektedir.
2. Hello kaynak makinede hello yürütülebilir çalıştırarak Hello Mobility hizmetini yükleyin.
3. Merhaba yükleyici yönergeleri izleyin.
4. Seçin **Mobility hizmeti** hello rolü ve tıklatın olarak **sonraki**.

    ![Mobilite hizmetinin yüklenmesi](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. Merhaba varsayılan yükleme yolu olarak Hello yükleme dizini bırakın ve tıklatın **yükleme**.
6. İçinde **konak Aracısı Yapılandırma** başlangıç IP adresi ve HTTPS bağlantı noktası hello yapılandırma sunucusu belirtin.

   * Internet belirtin hello bağlanıyorsanız genel sanal IP adresi ve ortak HTTPS uç noktası başlangıç bağlantı noktası olarak hello.
   * VPN üzerinden bağlanıyorsanız hello iç IP adresi ve başlangıç bağlantı noktası 443 belirtin. Bırakın **HTTPS kullan** işaretli.

     ![Mobilite hizmetinin yüklenmesi](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. Merhaba yapılandırma sunucusunun parolası belirtin ve tıklayın **Tamam** tooregister hello Mobility hizmeti ile Merhaba yapılandırma sunucusu.

**toorun hello komut satırından:**

1. Merhaba parola hello CX toohello dosyası "C:\connection.passphrase" Merhaba sunucusuna kopyalayın ve bu komutu çalıştırın. Örneğimizde CX i 104.40.75.37 hello HTTPS bağlantı noktası ise 62519:

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**Merhaba Mobility hizmeti el ile Linux sunucusu üzerinde yükleme**:

1. Yukarıdaki hello tabloya hello işlem sunucusu toohello kaynak makineden dayalı hello uygun tar arşiv kopyalayın.
2. Bir kabuk programı açmak ve yürüterek hello daraltılmış tar arşiv tooa yerel yol ayıklayın`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. Passphrase.txt dosyası oluşturma hello yerel dizin toowhich hello tar arşiv Merhaba içeriğine girerek ayıkladığınız  *`echo <passphrase> >passphrase.txt`*  Kabuğu'ndan.
4. Girerek Hello mobilite hizmetinin yüklenmesi  *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* .
5. Başlangıç IP adresi ve bağlantı noktasını belirtin:

   * Internet belirtin hello yapılandırma sunucusu sanal ortak IP adresi ve ortak HTTPS uç hello üzerinden toohello yapılandırma sunucusu bağlanıyorsanız `<IP address>` ve `<port>`.
   * Bir VPN bağlantısı üzerinden bağlanıyorsanız hello iç IP adresi ve 443 belirtin.

**Merhaba komut satırından toorun**:

1. Merhaba parola hello CX toohello dosyası "passphrase.txt" Merhaba sunucusuna kopyalayın ve bu komutları çalıştırın. Örneğimizde CX i 104.40.75.37 hello HTTPS bağlantı noktası ise 62519:

tooinstall bir üretim sunucusunda:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall hello hedef sunucuda:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> Ne zaman hello anında yükleme atlandı sonra zaten hello Mobility hizmeti uygun bir sürümünü çalıştıran makineler tooa koruma grubu ekleyin.
>
>

## <a name="step-9-enable-protection"></a>9. adım: Etkinleştirme koruma
tooenable koruma sanal makineleri ve fiziksel sunucuları tooa koruma grubuna ekleyin. Başlamadan önce dikkat edin:

* Sanal makineler 15 dakikada bir bulunan ve bunları too15 dakikadır yukarı alabilir bulma sonra Azure Site kurtarma tooappear.
* Ortam değişiklikleri (örneğin, VMware araçları yükleme) hello sanal makinede de Site Recovery güncelleştirilmiş too15 dakika toobe yukarı alabilir.
* Merhaba, başlangıç zamanında en son bulunan kontrol edebilirsiniz **en son kişi** hello üzerinde hello vCenter sunucusu/ESXi ana bilgisayar için alan **yapılandırma sunucularına** sayfa.
* Önceden oluşturulmuş bir koruma grubu varsa ve bundan sonra bir vCenter Server veya ESXi konağına eklemek ve sanal makineleri toobe hello listelenen hello Azure Site Recovery portalı toorefresh için beş dakika sürer **makineler tooa koruma grubu Ekle**  iletişim.
* Merhaba yapılandırma sunucusu için zamanlanmış bulma hello beklemeden makineler tooprotection grubu ekleme olmadan hemen tooproceed isterseniz vurgulayın (tıklatın yok) hello tıklatıp **Yenile** düğmesi.
* Sanal makineleri veya fiziksel makineler tooa koruma grubu eklediğinizde, hello işlem sunucusu otomatik olarak iter ve Merhaba, zaten yüklü değilse hello Mobility hizmeti hello kaynak sunucuda yükler.
* Merhaba otomatik itme mekanizması için toowork korumalı makinelerinizi hello önceki adımda açıklandığı şekilde ayarladığınızdan emin olun.

Makineler aşağıdaki şekilde ekleyin:

1. Tıklatın **korunan öğeleri** > **koruma grubu** > **makineler** > **makineleri ekleyin**. En iyi uygulama olarak belirli bir uygulama toohello çalışan makineler eklemek için koruma grupları, iş yüklerini yansıtmak olan öneririz aynı grubu.
2. İçinde **sanal makineleri seçin** hello fiziksel sunucuları koruyorsanız **eklemek fiziksel makineleri** Sihirbazı başlangıç IP adresi ve kolay bir ad sağlayın. Ardından hello işletim sistemi ailesi seçin.

    ![V merkezi sunucusu ekleme](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. İçinde **sanal makineleri seçin** VMware sanal makineleri koruyorsanız, sanal makineleri (veya bunlar çalışmakta olduğu hello EXSi konak) yönetme bir vCenter sunucusu seçin ve ardından hello makineleri seçin.

    ![V merkezi sunucusu ekleme](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. İçinde **belirtin hedef kaynaklar** hello ana hedef sunucu ve çoğaltma için depolama toouse ve hello ayarları tüm iş yükleri için kullanılması gereken olup olmadığını seçin. Seçin [Premium depolama hesabı](../storage/common/storage-premium-storage.md) tutarlı yüksek g/ç performans ve düşük gecikme sipariş toohost g/ç yoğun iş yükleri gerektiren iş yükleri için koruma yapılandırılırken. İş yükü diskleriniz için toouse bir Premium depolama hesabı istiyorsanız toouse hello DS serisi ana hedefinin gerekir. Premium depolama diskleri DS serisi ile ana hedef kullanamazsınız.

   > [!NOTE]
   > Merhaba taşıma hello kullanılarak oluşturulan depolama hesaplarının desteklemiyoruz [yeni Azure portalına](../storage/common/storage-create-storage-account.md) kaynak grupları arasında.
   >
   >

    ![vCenter sunucusu](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. İçinde **belirtin hesapları** hello Mobility hizmetinin korunan makinelere yüklemek için toouse istediğiniz hello hesabını seçin. Merhaba hesabı kimlik bilgileri otomatik hello mobilite hizmetinin yüklenmesi için gereklidir. Bir hesap emin seçemiyorsanız bir 2. adımda açıklandığı gibi ayarladığınız. Bu hesap Azure tarafından erişilen unutmayın. Windows server hello hesabı hello kaynak sunucuda yönetici ayrıcalıkları olması gerekir. Linux için kök hello hesabı olmalıdır.

    ![Linux kimlik bilgileri](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. Makineler toohello koruma grubu ve toostart ilk çoğaltma için her makine ekleme hello onay işareti toofinish'ı tıklatın. Merhaba durumunu izleyebilirsiniz **işleri** sayfası.

    ![V merkezi sunucusu ekleme](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. Ayrıca, tıklayarak koruma durumunu izleyebilirsiniz **korunan öğeler** > koruma grubu adı > **sanal makineleri** . İlk çoğaltma tamamlandıktan sonra hello makineler veri eşitleme gösterecektir **korumalı** durumu.

    ![Sanal makine işleri](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>Makine özelliklerini korumalı ayarlama
1. Bir makine sahip olduktan sonra bir **korumalı** durum yük devretme özelliklerini yapılandırabilirsiniz. Merhaba koruma grubu ayrıntılarını seçin makine ve açık hello hello **yapılandırma** sekmesi.
2. Yük devretme ve hello Azure sanal makine boyutu sonra toohello makine Azure'da verilen hello adını değiştirebilirsiniz. Öğesini de seçebilirsiniz hello Azure ağ toowhich hello makine yük devretme sonrasında bağlı.

   > [!NOTE]
   > [Geçiş ağların](../resource-group-move-resources.md) kaynak arasında grupları içinde hello aynı abonelik veya abonelikler arasında Site Recovery dağıtmak için kullanılan ağlar için desteklenmez.
   >
   >

    ![Sanal makine özelliklerini ayarla](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

Şunlara dikkat edin:

* hello Azure makine adını Hello Azure gereksinimlere uygun olmalıdır.
* Varsayılan olarak Azure çoğaltılmış sanal makinelere bağlı tooan Azure ağı değil. Çoğaltılmış sanal makinelere toocommunicate emin olmak istiyorsanız tooset hello aynı Azure ağ kendileri için.
* VMware sanal makineleri veya fiziksel sunucu üzerindeki bir birimi yeniden boyutlandırmak, kritik duruma geçer. Toomodify hello boyutu gerekiyorsa, aşağıdaki hello:

  * bir) hello boyutu ayarını değiştirin.
  * b) içinde hello **sanal makineleri** sekmesinde hello sanal makine seçin ve tıklatın **kaldırmak**.
  * c) içinde **sanal makineyi Kaldır** hello seçeneğini belirleyin **devre dışı bırakın (kurtarma için detaya kullanın ve birim yeniden boyutlandırma)**. Bu seçenek, korumayı devre dışı bırakır, ancak azure'da hello kurtarma noktalarını korur.

      ![Sanal makine özelliklerini ayarla](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d) hello sanal makine için korumayı yeniden etkinleştirin. Merhaba yeniden boyutlandırılmış birim için koruma hello verileri ne zaman yeniden etkinleştirmek aktarılan tooAzure olacaktır.

## <a name="step-10-run-a-failover"></a>10. adım: yük devretme gerçekleştirme
Şu anda yalnızca korumalı VMware sanal makineleri ve fiziksel sunucuları için planlanmamış yük devretmeler çalıştırabilirsiniz. Merhaba aşağıdakileri göz önünde bulundurun:

* Bir yük devretme başlatın önce hello yapılandırma ve ana hedef sunucularının çalıştığından ve sağlıklı olduğundan emin olun. Aksi takdirde yük devretme başarısız olur.
* Planlanmamış bir yük devretme bir parçası olarak kaynak makineleri kapatmaya değil. Planlanmamış bir yük devretme gerçekleştirme hello korunan sunucular için veri çoğaltma durur. Merhaba koruma grubundan toodelete hello makinelerin gerekir ve bunları yeniden hello planlanmamış yük devretme tamamlandıktan sonra makineleri yeniden koruma sipariş toostart içinde Ekle.
* Toofail üzerinden herhangi bir veri kaybetmeden isterseniz, hello yük devretme başlatmadan önce hello birincil site sanal makineleri kapalı olduğundan emin olun.

1. Merhaba üzerinde **kurtarma planları** sayfasında ve bir kurtarma planı ekleyin. Merhaba plan ayrıntılarını belirtin ve seçin **Azure** hello hedefi olarak.

    ![Kurtarma planı yapılandırın](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. İçinde **sanal makineyi Seç** bir koruma grubu seçin ve ardından hello Grup tooadd toohello kurtarma planındaki makineleri seçin. [Daha fazla bilgi](site-recovery-create-recovery-plans.md) kurtarma planları hakkında.

    ![Sanal makineleri ekleyin](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. Merhaba plan toocreate gruplarını ve sırası hello sırası özelleştirebileceğiniz hangi makinelerde hello kurtarma planı yük devredildi durumunda. El ile gerçekleştirilen eylemleri ve komut dosyaları da ekleyebilirsiniz. tooAzure kurtarma kullanılarak eklenebilir, komut dosyaları Hello [Azure Automation Runbook](site-recovery-runbook-automation.md).
4. Merhaba, **kurtarma planları** sayfa seç hello planı ve tıklatın **planlanmamış yük devretme**.
5. İçinde **onaylayın yük devretme** hello yük devretme yönü (tooAzure) doğrulayın ve hello kurtarma noktası toofail üzerinden seçin.
6. Merhaba yük devretme iş toocomplete için bekleyin ve ardından hello yük devretme beklendiği gibi çalıştığını ve o hello Azure'nın başarıyla sanal makineleri Başlat çoğaltılan doğrulayın.

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>11. adım: Azure makinelerden geri devredilir başarısız
[Daha fazla bilgi edinin](site-recovery-failback-azure-to-vmware-classic-legacy.md) konusunda toobring, başarısız tooyour şirket içi ortamına geri Azure'da çalışan makineler üzerinden.

## <a name="manage-your-process-servers"></a>İşlem sunucularınızı yönetin
Merhaba işlem sunucusu Azure içinde çoğaltma veri toohello ana hedef sunucusuna gönderir ve yeni VMware sanal makineleri eklenen tooa vCenter sunucusu bulur. Aşağıdaki durumlarda hello dağıtımınızda toochange hello işlem sunucusu isteyebilirsiniz:

* Merhaba geçerli işlem sunucusu kullanılamaz hale gelirse
* Kurtarma noktası hedefi (RPO) kuruluşunuz için kabul edilebilir düzeyi tooan artar.

Merhaba çoğaltmasını bazılarını veya tümünü, şirket içi VMware sanal taşıyabilirsiniz gerekirse makineleri ve fiziksel sunucuları tooa farklı sunucu işlemleri. Örneğin:

* **Hata**— bir işlem sunucusu başarısız olduğunda veya kullanılabilir değil, korumalı makine çoğaltma tooanother işlem sunucusu taşıyabilirsiniz. Verileri yeniden eşitlenmesi ve meta veri hello kaynak makine ve çoğaltma makinesi taşınan toohello yeni işlem sunucusu olacaktır. Merhaba yeni işlem sunucusu toohello vCenter server tooperform otomatik bulma otomatik olarak bağlanır. Merhaba Site Recovery Pano işlemi sunucularda hello durumunu izleyebilirsiniz.
* **Yük Dengeleme tooadjust RPO**— Gelişmiş bir Yük Dengeleme, hello Site kurtarma Portalı'nda farklı bir işlem sunucusu seçin ve el ile Yük Dengeleme için bir veya daha fazla makineler tooit çoğaltmasını taşıyın. Bu durumda hello seçilen kaynak ve çoğaltma makinelerini meta verileri taşınan toohello yeni işlem sunucusu olur. Merhaba özgün işlem sunucusuna bağlı toohello vCenter sunucusu kalır.

### <a name="monitor-hello-process-server"></a>İzleyici hello işlem sunucusu
Kritik durumdaki bir işlem sunucusu ise, Site kurtarma Pano hello üzerinde durumu uyarısı görüntülenir. Merhaba durum tooopen hello olayları sekmesine tıklayın ve toospecific işleri hello işler sekmesinde detaya.

### <a name="modify-hello-process-server-used-for-replication"></a>Çoğaltma için kullanılan hello işlem sunucusunu değiştirme
1. Açık **sunucuları** > **yapılandırma sunucularına** > yapılandırma sunucusu > **sunucu ayrıntıları**.
2. Tıklatın **işlem sunucuları** > **işlem sunucusunu Değiştir** toomodify istediğiniz sonraki toohello sunucu.

    ![İşlem sunucusunu Değiştir 1](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. İçinde **işlem sunucusunu Değiştir** > **hedef işlem sunucusunu** hello toouse istediğiniz ve hello sanal makineleri tooreplicate toohello yeni sunucu istediğiniz ardından yeni sunucu seçin. Merhaba bilgi simgesi sonraki toohello sunucu adı boş ve kullanılan bellek Ayrıntılar için tıklatın. Görüntülenen toohelp kararları yükleme yaptığınız her seçili sanal makine toohello yeni işlem sunucusu olan gerekli tooreplicate olacak hello ortalama alanı.

    ![İşlem sunucusunu Değiştir 2](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. Toohello yeni işlem sunucusu çoğaltma hello onay işareti toobegin'ı tıklatın. Tüm sanal makineleri kritik bir işlem sunucusundan kaldırırsanız, artık bir kritik uyarı hello panosunda görüntülemesi gerektiğini unutmayın.

## <a name="third-party-software-notices-and-information"></a>Üçüncü taraf yazılım uyarılar ve bilgiler
Sağlamadığı Çevir veya yerelleştirme

Merhaba yazılımını ve bellenimini çalışır durumda hello Microsoft Ürün veya hizmet dayanır veya hello malzemesini içerir projeleri listelenen (topluca "üçüncü taraf kodu").  Microsoft, hello hello üçüncü taraf kodu değil özgün yazarı.  Hello özgün telif hakkı bildirimi ve lisansı altında Microsoft gibi üçüncü taraf kodu alındı, aşağıda belirtilen ayarlanır.

Bir bölümdeki Hello bilgiler üçüncü taraf bileşenleri hello projelerden aşağıda listelenen kod ilgili olduğu. Bu tür lisansları ve bilgi yalnızca bilgilendirme amacıyla sağlanır.  Bu üçüncü taraf kodu Microsoft yazılım lisans hello Microsoft Ürün veya hizmet koşulları altında Microsoft tarafından relicensed tooyou yapılıyor.  

Bölüm B Hello bilgilerinde kullanılabilir tooyou hello özgün lisans şartları altında Microsoft tarafından kurulan üçüncü taraf kodu bileşenleri ilgili olduğu.

Merhaba tam dosya hello üzerinde bulunan [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft tarafından uygulanır olup olmadığını, belirtilmeyen tüm hakları ayırır rıza ya da aksi takdirde.
