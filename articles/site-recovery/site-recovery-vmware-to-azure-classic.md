---
title: "VMware Vm'lerini ve fiziksel sunucuları Klasik portalda Azure'a çoğaltma | Microsoft Docs"
description: "Bu makalede, çoğaltma, yük devretme ve kurtarma şirket içi VMware sanal makinelerin ve Windows/Linux fiziksel sunucuları azure'a düzenlemek için Azure Site Recovery dağıtmayı açıklar."
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
ms.openlocfilehash: 73c3fb5cf4056ddb9554f598ec7f173d81802f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-to-azure-with-azure-site-recovery"></a>VMware sanal makineleri ve fiziksel sunucuları Azure Site Recovery ile Azure'a çoğaltma
> [!div class="op_single_selector"]
> * [Azure portalı](site-recovery-vmware-to-azure.md)
> * [Klasik portal](site-recovery-vmware-to-azure-classic.md)
> * [Klasik Portalı'nı (eski)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Azure Site Recovery hizmeti, çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenleyerek iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar. Makineler, azure'a veya ikincil şirket içi veri merkezine çoğaltılabilir. Hızlı bir genel bakış için bkz: [Azure Site Recovery nedir?](site-recovery-overview.md).

## <a name="overview"></a>Genel Bakış
Bu makalede nasıl yapılır:

* **VMware sanal makinelerini Azure'a çoğaltma**: çoğaltma, yük devretme ve şirket içi VMware sanal makineleri kurtarma Azure depolama koordine etmek için Site Recovery dağıtın.
* **Fiziksel sunucuları Azure'a çoğaltma**: çoğaltma, yük devretme ve kurtarma, şirket içi fiziksel Windows ve Linux sunucularının Azure koordine etmek için Azure Site Recovery dağıtın.

> [!NOTE]
> Bu makalede, azure'a açıklar. VMware Vm'leri veya Windows/Linux fiziksel sunucuları ikincil bir veri merkezine çoğaltmak istiyorsanız, bkz: [Site kurtarma Vmware'den vmware'e](site-recovery-vmware-to-vmware.md).
>
>

Tüm yorumlarınızı ve sorularınızı bu makalenin veya üzerinde altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Gelişmiş dağıtım
Bu makale, Azure Klasik Portalı'nda gelişmiş bir dağıtımı için yönergeler içerir. Tüm yeni dağıtımlar için bu sürümünü kullanmanızı öneririz. Önceki eski sürümünü kullanarak zaten dağıttıktan sonra yeni sürüme yükseltmenizi öneririz. Geçiş hakkında daha fazla bilgi için bkz: [Azure Klasik eski Site kurtarma VMware](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

Gelişmiş dağıtıma önemli bir güncelleştirmedir. Geliştirmeler yaptık bir özeti aşağıda verilmiştir:

* **Hiçbir altyapı azure'da Vm'leri**: verilerini doğrudan bir Azure depolama hesabı çoğaltır. Ayrıca, herhangi bir altyapı VM'ler (yapılandırma sunucusu veya ana hedef sunucusu gibi) çoğaltma ve yük devretme için eski dağıtımda gerektiğinde ayarlamak için gerek yoktur.  
* **Birleşik yükleme**: tek bir yüklemede basit kurulumu ve şirket içi bileşenleri için ölçeklenebilirlik sağlar.
* **Dağıtımınızın güvenliğini**: tüm trafiği şifrelenir ve çoğaltma yönetim iletişimleri HTTPS 443 üzerinden gönderilir.
* **Kurtarma noktaları**: desteği kilitlenme ve uygulamaları tutarlı kurtarma noktaları Windows ve Linux ortamlar için ve her ikisi de tek bir VM ve çoklu VM tutarlı yapılandırmaları için destek.
* **Yük devretme sınamasını**: benzer test yük devretmesi etkilemeden üretim veya çoğaltma duraklatma olmadan Azure için destek.
* **Planlanmamış yük devretme**: VM'ler önce yük devretme otomatik olarak kapatmak için Gelişmiş bir seçenek ile Azure planlanmamış yük devretme için destek.
* **Yeniden çalışma**: şirket içi siteye yalnızca delta değişiklikler çoğaltılır tümleşik geri dönme.
* **vSphere 6.0**: sınırlı VMware vSphere 6.0 dağıtımları için destek.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Site Recovery sanal makineleri ve fiziksel sunucuları korumaya nasıl yardımcı olur?
* VMware kurumsal iş yükleri ve VMware sanal makinelerde çalışan uygulamaların Azure korumak için site dışındaki korumaları yapılandırabilirler. Sunucu yöneticileri fiziksel şirket içi Windows ve Linux sunucuları Azure'a çoğaltabilirsiniz.
* Azure Site Kurtarma Konsolu basit kurulum ve yönetim çoğaltma, yük devretme ve kurtarma işlemleri için tek bir konum sağlar.
* Bir vCenter sunucusu tarafından yönetilen bir VMware sanal makineleri çoğaltmak, Site Recovery bu sanal makineleri otomatik olarak bulabilir. Makineler ESXi ana bilgisayarda varsa, Site Recovery ana bilgisayarda sanal makineleri bulur.
* Şirket içi altyapınızdan Azure'a kolay yük devretme çalıştırırsanız başarısız olabilir () Azure'dan şirket içi sitede VMware VM sunucularına geri.
* Birden fazla makine arasında katmanlı uygulama iş yüklerini grup kurtarma planlarını yapılandırabilirsiniz. Bu planlara başarısız olursa, Site Recovery aynı iş yüklerini çalıştıran makineler birlikte bir tutarlı veri noktasına kurtarılabilen çoklu VM tutarlılığı sağlar.

## <a name="supported-operating-systems"></a>Desteklenen işletim sistemleri
### <a name="windows-64-bit-only"></a>Windows (yalnızca 64 bit)
* Windows Server 2008 R2 SP1 +
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (yalnızca 64 bit)
* Red Hat Enterprise Linux 7.2 6.7 ve 7.1
* CentOS 6.5, 6.6, 6.7, 7.0, 7.1 ve 7.2
* Oracle Enterprise Linux 6.4 ve Red Hat uyumlu çekirdek ya da kesilemeyen kurumsal çekirdek sürüm 3 (UEK3) çalıştıran 6.5
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>Senaryo mimarisi
Senaryo Bileşenleri:

* **Bir şirket içi yönetim sunucusu**: Site Recovery bileşenleri yönetim sunucusu çalışır:
  * **Yapılandırma sunucusu**: iletişimi düzenler ve veri çoğaltma ve kurtarma işlemlerini yönetir.
  * **İşlem sunucusu**: çoğaltma ağ geçidi olarak davranır. Korumalı kaynak makinelerden veri aldığı; önbelleğe alma, sıkıştırma ve şifreleme iyileştirir; ve Azure depolama çoğaltma verileri gönderir. Ayrıca Mobility hizmetinin korunan makinelere göndermeli yüklemesini işler ve VMware vm'lerinin otomatik bulma işlemini gerçekleştirir.
  * **Ana hedef sunucusu**: Azure'dan yeniden çalışma sırasında çoğaltma verilerini işler.
    Dağıtımınız ölçeklendirmek için yalnızca bir işlem sunucusu gibi davranan bir yönetim sunucusu da dağıtabilirsiniz.
* **Mobility hizmetinin**: Bu bileşen Azure'a çoğaltmak istediğiniz her makinede (VMware VM veya fiziksel sunucusu) dağıtılır. Yakalar makinede veri yazar ve işlem sunucusuna gönderir.
* **Azure**: herhangi bir Azure VM çoğaltma ve yük devretme işlemek için oluşturmanız gerekmez. Veri Yönetimi Site Recovery hizmetini işleme ve verileri doğrudan Azure depolama alanına çoğaltır. Yalnızca azure'a yük devretme durumunda çoğaltılan Azure Vm'leri çalışmaya otomatik olarak başlar. Ancak, şirket içi sitede yeniden çalıştırmak istiyorsanız, bir Azure VM'yi yedekleme işlem sunucusu olarak davranacak şekilde ayarlamanız gerekir.

Bu bileşenlerin nasıl etkileşim (Henry Robalino tarafından oluşturulan) aşağıdaki grafikte gösterir:

![Bileşen mimarisi](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Kapasite planlaması
Ne zaman yapılandırmanızda gerekenler kapasite, burada 's planlıyorsanız:

* **Kaynak ortamı**: kapasite planlaması veya VMware altyapı ve kaynak makine gereksinimleri.
* **Yönetim sunucusu**: Site Recovery bileşenlerini çalıştıran şirket içi yönetim sunucuları için planlama.
* **Hedef kaynağından ağ bant genişliği**: kaynak ve Azure arasında çoğaltma için gereken ağ bant genişliğini planlama.

### <a name="source-environment-considerations"></a>Kaynak ortamı konuları
* **Maksimum günlük değişim oranı**: bir korumalı makine yalnızca bir işlem sunucusu kullanabilirsiniz. Tek bir işlem sunucusu veri değişikliği günde en fazla 2 TB işleyebilir. Bu nedenle, 2 TB maksimum günlük veri korumalı bir makine için desteklenen oranı değiştirmektir.
* **En yüksek verimlilik**: çoğaltılmış bir makineden azure'da bir depolama hesabına ait olabilir. Standart depolama hesabı 20.000 istekleri saniye başına maksimum işleyebilir ve kaynak makine arasında IOPS sayısı 20,000 ile tutmanızı öneririz. Örneğin, kaynak makine 5 disklerle varsa ve her disk kaynağı 120 IOPS (8 KB boyutu) oluşturur, bunu Azure başına 500 disk IOPS sınırı içinde olacaktır. Sayı gerekli depolama hesaplarının toplam kaynak IOP/20, 000 =.

### <a name="management-server-considerations"></a>Yönetim sunucusu değerlendirmeleri
Yönetim sunucusu veri en iyi duruma getirme, çoğaltma ve yönetim işleyen Site Recovery bileşenlerini çalıştırır. Korumalı makineler üzerinde çalışan tüm iş yükleri arasında günlük değişikliği oranı kapasite işleyebilen olmalıdır ve sürekli olarak verileri Azure depolama alanına çoğaltmak için yeterli bant genişliği sahiptir. Bu avantajlar şunlardır:

* İşlem sunucusu korunan makinelerden çoğaltma verilerini alıp ve önbelleğe alma, sıkıştırma ve şifreleme için Azure göndermeden önce iyileştirir. Yönetim sunucusu, bu görevleri gerçekleştirmek için yeterli kaynak olması gerekir.
* İşlem sunucusu disk tabanlı önbelleği kullanır. 600 GB veya daha fazla ağ sorununu veya kesinti durumunda depolanan veri değişikliklerini işlemek için ayrı önbelleği disk öneririz. Dağıtım sırasında önbellek en az 5 GB depolama alanı kullanılabilir olan herhangi bir sürücüde yapılandırabilirsiniz, ancak 600 GB minimum önerilir.
* En iyi uygulama, yönetim sunucusu aynı ağ ve LAN kesimi korumak istediğiniz makinelere bulunduğu öneririz. Farklı bir ağda bulunan, ancak korumak istediğiniz makinelere L3 ağ görünürlük ona sahip olmalıdır.

Boyut önerileri yönetim sunucusu aşağıdaki tabloda özetlenmiştir:

| **Yönetim sunucusu CPU** | **Bellek** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler** |
| --- | --- | --- | --- | --- |
| 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek) |16 GB |300 GB |500 GB veya daha az |100'den az makineleri çoğaltmak için bu ayarlara sahip bir yönetim sunucusu dağıtın. |
| 12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) |18 GB |600 GB |1 TB ' 500 GB |100-150 makineleri çoğaltmak için bu ayarlara sahip bir yönetim sunucusu dağıtın. |
| 16 Vcpu (2 yuva * 2,5 GHz @ 8 çekirdek) |32 GB |1 TB |1 TB ile 2 TB |150-200 makineleri çoğaltmak için bu ayarlara sahip bir yönetim sunucusu dağıtın. |
| Başka bir işlem sunucusu Dağıt | | |> 2 TB |Ek işlem sunucusu 200'den fazla makineleri çoğaltma yapıyorsanız ya da günlük verileri değiştirirseniz oranı 2 TB aştığında dağıtın. |

Konumlar:

* Her kaynak makine 3 100 GB disk ile yapılandırılır.
* 8 SAS sürücüleri 10.000 RPM Kıyaslama depolanmasını RAID 10 ile için önbellek disk ölçümleri kullandık.

### <a name="network-bandwidth-from-source-to-target"></a>Hedef kaynağından ağ bant genişliği
Kullanarak ilk çoğaltma ve değişim çoğaltması için gerekli olacak bant genişliğini hesaplamak emin olun [kapasite planlayıcısı aracı](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Çoğaltma için kullanılan bant genişliği azaltma
Azure'a kopyalanan VMware trafiği belirli işlem sunucusu üzerinden gider. Site Recovery çoğaltma bu sunucu üzerinde aşağıdaki gibi kullanılabilir bant genişliğini kısıtlayabilirsiniz:

1. Açık Microsoft Azure Backup MMC ek bileşenini ana yönetim sunucusuna veya ek çalıştıran yönetim sunucusu üzerinde işlem sunucuları sağlandı. Varsayılan olarak, Microsoft Azure yedekleme için bir kısayol masaüstünde oluşturulur. Veya, C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin içinde yolunda bulabilirsiniz.
2. Ek bileşende **Özellikleri Değiştir**'e tıklayın.

    ![Bant genişliği Özellikleri Değiştir kısıtlama](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Üzerinde **azaltma** sekmesinde, Site Recovery çoğaltma ve geçerli zamanlama için kullanılabilir bant genişliğini belirtin.

    ![Çoğaltma bant genişliği azaltma](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

PowerShell kullanarak azaltma de ayarlayabilirsiniz. Örnek aşağıda verilmiştir:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Bant genişliği kullanımını en üst düzeye çıkarma
Çoğaltma için Azure Site Recovery tarafından kullanılan bant genişliğini artırmak için bir kayıt defteri anahtarını değiştirmeniz gerekir.

Aşağıdaki anahtarı çoğaltırken kullanılan disk çoğaltma başına iş parçacığı sayısını denetler:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 Fazla sağlanan bir ağda, bu kayıt defteri anahtarı kendi varsayılan değerlerinin değiştirilmesi gerekiyor. En fazla 32 destekliyoruz.  

Ayrıntılı kapasite planlaması hakkında daha fazla bilgi için bkz: [Site Recovery kapasite Planlayıcısı](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Ek işlem sunucuları
200'den fazla makine ya da günlük değişikliği hızınızı korumanız gerekiyorsa 2 TB yükünü işlemek için ek sunucular ekleyebilirsiniz daha büyük. Genişletmek için şunları yapabilirsiniz:

* Yönetim sunucularının sayısını artırın. Örneğin, iki yönetim sunucuları ile en fazla 400 makineler koruyabilirsiniz.
* Ek işlem sunucusu ekleyin ve bunlar yerine (veya ek olarak) trafiğini işlemek için kullanmak yönetim sunucusu.

Bu tabloda bir senaryoda açıklanmıştır:

* Özgün yönetim sunucusu, yalnızca bir yapılandırma sunucusu olarak kullanacak şekilde ayarlayın.
* Bir ek işlem sunucusu ayarlayın.
* Korumalı sanal makineleri ek işlem sunucusu kullanacak şekilde yapılandırın.
* Her korumalı kaynak makine üç 100 GB disk ile yapılandırılır.

| **Özgün yönetim sunucusu**<br/><br/>(yapılandırma sunucusu) | **Ek işlem sunucusu** | **Önbellek disk boyutu** | **Veri değişikliği oranı** | **Korumalı makineler** |
| --- | --- | --- | --- | --- |
| 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 16 GB RAM |4 Vcpu (2 yuva * 2,5 GHz @ 2 Çekirdek), 8 GB RAM |300 GB |250 GB veya daha az |85 veya daha az makineleri çoğaltabilirsiniz. |
| 8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 16 GB RAM |8 Vcpu'lar (2 yuva * @ 2,5 GHz 4 çekirdek), 12 GB RAM |600 GB |1 TB ' 250 GB |85 150 makineleri çoğaltabilirsiniz. |
| 12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek), 18 GB RAM |12 Vcpu'lar (2 yuva * 2,5 GHz @ 6 çekirdek) 24 GB RAM |1 TB |1 TB ile 2 TB |150-225 makineleri çoğaltabilirsiniz. |

Sunucularınızın ölçeklendirme nasıl büyütme veya genişleme modeli için tercihinizi bağlıdır. Birkaç Gelişmiş Yönetim ve işlem sunucuları dağıtarak ölçeği veya daha az kaynak ile daha fazla sunucu dağıtarak ölçeğini. Örneğin: 220 makinelerin korunmasına ihtiyacınız varsa, aşağıdakilerden birini yapabilirsiniz:

* Özgün yönetim sunucusu 12 Vcpu'lar ve 18 GB RAM yapılandırın. Bir ek işlem sunucusu 12 Vcpu'lar ve 24 GB RAM yapılandırın. Korumalı makineler, yalnızca ek işlem sunucusu kullanacak şekilde yapılandırın.
* İki yönetim sunucuları (2 x 8 Vcpu, 16 GB RAM) ve iki ek işlem sunucusu (1 x 8 Vcpu'lar ve 4vCPUs 135 + 85 (220) makineler işlemek için 1 x) yapılandırın. Korumalı makineler, yalnızca ek işlem sunucularını kullanacak şekilde yapılandırın.

' Ndaki yönergeleri izleyin [ek işlem sunucusu dağıtın](#deploy-additional-process-servers) bir ek işlem sunucusu ayarlanamıyor.

## <a name="before-you-start-deployment"></a>Dağıtıma başlamadan önce
Aşağıdaki tablolarda, bu senaryoyu dağıtmak için önkoşullar özetlenmektedir.

### <a name="azure-prerequisites"></a>Azure önkoşulları
| **Önkoşul** | **Ayrıntılar** |
| --- | --- |
| **Azure hesabı** |Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Site Recovery fiyatlandırması hakkında daha fazla bilgi için bkz: [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Azure depolama alanı** |Çoğaltılan verileri depolamak için bir Azure depolama hesabınızın olması gerekir. Çoğaltılan veriler Azure depolama alanında depolanır ve yük devretme durumunda Azure Vm'leri çalışmaya başlar. <br/><br/>[Standart coğrafi olarak yedekli depolama hesabınızın](../storage/storage-redundancy.md#geo-redundant-storage) olması gerekir. Hesabın Site Recovery hizmeti ile aynı bölgede olması ve aynı abonelikle ilişkilendirilmiş olması gerekir. Premium depolama hesapları için çoğaltma şu anda desteklenmiyor ve kullanılmamalıdır.<br/><br/>Taşıma depolama hesapları kullanılarak oluşturulan desteklemiyoruz [Azure portal](../storage/storage-create-storage-account.md) kaynak grupları arasında. Daha fazla bilgi için bkz: [Microsoft Azure Storage'a giriş](../storage/storage-introduction.md).<br/><br/> |
| **Azure ağı** |Yük devretme durumunda Azure makinelerinin bağlanacağı bir Azure sanal ağı gerekir. Azure sanal ağının Site Recovery kasasıyla aynı bölgede olması gerekir.<br/><br/>Bir VPN ihtiyacınız geri azure'a yük devretme sonrasında başarısız olmasına bağlantısı (veya Azure ExpressRoute) ayarlama Azure ağından şirket içi siteye. |

### <a name="on-premises-prerequisites"></a>Şirket içi önkoşullar
| **Önkoşul** | **Ayrıntılar** |
| --- | --- |
| **Yönetim sunucusu** |Bir sanal makine ya da fiziksel sunucu üzerinde çalışan bir şirket içi Windows 2012 R2 sunucusu gerekir. Tüm şirket içi Site Recovery bileşenlerini bu yönetim sunucusuna yüklenir.<br/><br/> Sunucunun yüksek oranda kullanılabilir bir VMware VM olarak dağıttığınız öneririz. Azure'dan şirket içi siteye her zaman VMware Vm'lerinde olup, sanal makineleri veya fiziksel sunucular üzerinden başarısız bağımsız olarak olduğu. VMware VM olarak Yönetim Sunucusu yapılandırmazsanız, yeniden çalışma trafiği almak için VMware VM olarak bir ayrı ana hedef sunucusu ayarlamanız gerekir.<br/><br/>Sunucu bir etki alanı denetleyicisi olmaması gerekir.<br/><br/>Sunucunun bir statik IP adresi olmalıdır.<br/><br/>Sunucunun ana bilgisayar adı 15 karakter uzunluğunda olmalıdır veya daha az.<br/><br/>Yalnızca işletim sistemi yerel ayarı İngilizce olmalıdır.<br/><br/>Yönetim sunucusunun Internet erişimi gerektirir.<br/><br/>Giden sunucudan gibi erişmeniz: HTTP 80 üzerinde geçici erişim (MySQL indirmek için) Site Recovery bileşenlerini; kurulumu sırasında çoğaltma yönetimi için HTTPS 443 üzerinde devam eden giden erişim; çoğaltma trafiği (Bu bağlantı noktası değiştirilebilir) için HTTPS 9443 üzerinde devam eden giden erişim.<br/><br/> Bu URL'leri yönetim sunucusundan erişilebilir olduğundan emin olun: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>-https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.MySQL.com/Get/Archives/MySQL-5.5/MySQL-5.5.37-Win32.msi](https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Sunucuda IP adresi tabanlı güvenlik duvarı kuralları varsa, kuralları Azure ile iletişim kurmaya izin verdiğinden emin olun. [Azure Veri Merkezi IP Aralıkları](https://www.microsoft.com/download/details.aspx?id=41653)'na ve HTTPS (443) bağlantı noktasına izin vermeniz gerekir. Beyaz liste IP adres aralıklarını aboneliğinizin Azure bölgesi ve Batı ABD için gerekir. URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi](https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") MySQL yüklemek için değil. |
| **VMware vCenter/ESXi ana bilgisayar** |ESX/ESXi sürüm 6.0, 5.5 veya 5.1 ile en son güncelleştirmeleri çalıştıran, VMware sanal makineleri yönetme bir veya daha fazla VMware vSphere ESX/ESXi hiper gerekir.<br/><br/> ESXi ana bilgisayarları yönetmek için bir VMware vCenter sunucusu dağıtmanızı öneririz. En son güncelleştirmelerine sahip vCenter sürüm 6.0 veya 5.5 çalışmalıdır.<br/><br/>Site Recovery yeni vCenter desteklemez ve vSphere 6.0 özellikleri gibi vCenter VMotion'ı, sanal birimler ve depolama DRS arası unutmayın. Site kurtarma desteği de 5.5 sürümünde kullanılabilir özellikler sınırlıdır. |
| **Korumalı makineler** |**Azure**<br/><br/>Korumak istediğiniz makinelere ile uygun olması [Azure önkoşulları](site-recovery-prereq.md) Azure sanal makineleri oluşturmak için.<br><br/>Yük devretme sonrasında Azure Vm'lerine bağlanmak isterseniz, Yerel Güvenlik Duvarı'nda Uzak Masaüstü bağlantılarını etkinleştirmeniz gerekir.<br/><br/>Korumalı makinelerdeki bağımsız disk kapasitesinin 1023 GB'tan fazla olmaması gerekir. Bir VM 64 adede kadar disk barındırabilir (64 TB'ye kadar). 1 TB'den büyük olan diskler varsa, veritabanı çoğaltması SQL Server Always On veya Oracle Data Guard gibi kullanmayı düşünün.<br/><br/>Bileşen yüklemesi için yükleme sürücüsünde kullanılabilir alan en az 2 GB.<br/><br/>Paylaşılan disk konuk kümeleri desteklenmez. Kümelenmiş bir dağıtımınız varsa, veritabanı çoğaltması SQL Server Always On veya Oracle Data Guard gibi kullanmayı düşünün.<br/><br/>Birleşik Genişletilebilir Bellenim Arabirimi (UEFI) / Genişletilebilir Bellenim EFI önyükleme desteklenmez.<br/><br/>Makine adı 1 ile 63 karakter arasında (harf, rakam ve kısa çizgi) içermelidir. Adı bir harf veya sayı ile başlamalı ve bir harf veya sayı ile bitmelidir. Bir makine korunduktan sonra Azure ad değiştirebilirsiniz.<br/><br/>**VMware Vm'leri**<br/><br>VMware vSphere Powerclı 6.0 yüklemeniz gerekir. Yönetim sunucusunda (yapılandırma sunucusu).<br/><br/>VMware Vm'leri korumak istediğiniz VMware araçları yüklü ve çalışıyor olması gerekir.<br/><br/>Kaynak VM NIC ekibi oluşturma varsa, Azure yük devretme işleminin ardından tek bir NIC'ye dönüştürülür.<br/><br/>Korumalı VM'lerin bir iSCSI diski varsa, Site Recovery korumalı VM iSCSI disk için Azure üzerinden VM başarısız olduğunda bir VHD dosyasına dönüştürür. İSCSI hedef Azure VM tarafından erişilebilir değilse, iSCSI hedefine bağlanmak ve temelde iki disk bkz: Azure VM ve kaynak iSCSI disk VHD diski. Bu durumda, başarısız üzerinden Azure VM'de görünür iSCSI hedefi kesmeniz gerekir.<br/><br/>VMware kullanıcı izinleri hakkında daha fazla bilgi için Site kurtarma, bkz: gereken [VMware vCenter erişim izinlerini](#vmware-permissions-for-vcenter-access).<br/><br/> **Windows Server makinelerde (VMware VM veya fiziksel sunucu)**<br/><br/>Sunucu desteklenen bir 64-bit işletim sistemi çalıştırması gerekir: Windows Server 2012 R2, Windows Server 2012 veya Itanium tabanlı sistemler için Windows Server 2008 R2 ile en az SP1.<br/><br/>İşletim sistem C sürücüsünde yüklenmelidir ve işletim sistemi diski Windows temel disk olması gerekir. (İşletim sistemi bir Windows dinamik diske yüklenmesi gerekir.)<br/><br/>Windows Server 2008 R2 makineler için .NET Framework 3.5.1 yüklü olması gerekir.<br/><br/>Bir yönetici hesabı sağlamanız gerekir (Windows makinesinde yerel yönetici olması gerekir) Windows sunucularında mobilite hizmetinin göndermeli yüklemesi için. Sağlanan hesap bir etki alanı dışı hesabı ise, yerel makinede uzak kullanıcı erişim denetimi devre dışı bırakmanız gerekir. Daha fazla bilgi için bkz: [mobilite hizmetinin göndermeli yüklemesi ile yüklenmek](#install-the-mobility-service-with-push-installation).<br/><br/>Site Kurtarma ile RDM diski Vm'leri destekler. Yeniden çalışma sırasında RDM diski ve özgün kaynak VM mevcutsa, Site Recovery RDM diski yeniden kullanır. Yeniden çalışma sırasında kullanılabilir durumda değilse, Site Recovery her disk için yeni bir VMDK dosyasını oluşturun.<br/><br/>**Linux makineler**<br/><br/>Desteklenen bir 64-bit işletim sistemi gerekir: Red Hat Enterprise Linux 6.7; Centos 6.5, 6.6 veya 6.7; Oracle Enterprise Linux 6.4 veya Red Hat uyumlu çekirdek ya da kesilemeyen kurumsal çekirdek sürüm 3 (UEK3); çalıştıran 6.5 SUSE Linux Enterprise Server 11 SP3.<br/><br/>korumalı makinelerdeki/Etc/Hosts dosyaları, yerel ana bilgisayar adı tüm ağ bağdaştırıcıları ile ilişkili IP adreslerini eşlemek giriş içermelidir. <br/><br/>Secure Shell istemcisi (ssh) kullanarak yük devretme sonrasında Linux çalıştıran bir Azure sanal makinesine bağlanmak istiyorsanız, korumalı makine Secure Shell hizmetinin sistem önyüklemesinde otomatik olarak başlamaya ayarlanmıştır ve güvenlik duvarı kuralları izin sağlamak bir ssh bağlantı.<br/><br/>Koruma yalnızca etkinleştirilebilir aşağıdaki depolama ile Linux makineler için: dosya sistemi (EXT3, ETX4, ReiserFS, XFS); Çok yollu yazılım-aygıtı Eşleyici (çok yollu); Birim Yöneticisi (LVM2). HP CCISS denetleyicisi depolama ile fiziksel sunucuları desteklenmez. ReiserFS dosya sistemi yalnızca SUSE Linux Enterprise Server 11 SP3 üzerinde desteklenir.<br/><br/>Site Kurtarma ile RDM diski Vm'leri destekler. Linux için yeniden çalışma sırasında Site Recovery RDM diski yeniden kullanmaz. Bunun yerine, karşılık gelen her RDM diski için yeni bir VMDK dosyası oluşturur. |

Yalnızca bir Linux VM için: VMware VM'nin yapılandırma parametrelerini disk.enableUUID=true ayarı kümesindeki emin olun. Bu satır mevcut değilse, bunu ekleyin. Bu, böylece doğru bağlar tutarlı UUID VMDK'ye sağlamak için gereklidir. VM içi kullanılabilir olsa bile, bu ayar olmadan tam yükleme geri dönme neden olur. Bu ayarı ekleme, yalnızca delta değişiklikler geri yeniden çalışma sırasında aktarılmasını sağlar.

## <a name="step-1-create-a-vault"></a>1. adım: bir kasa oluşturma
1. [Azure Portal](https://manage.windowsazure.com/) oturum açın.
2. Genişletme **Veri Hizmetleri** > **kurtarma Hizmetleri** tıklatıp **Site Recovery kasası**.
3. **Yeni Oluştur** > **Hızlı Oluştur**'a tıklayın.
4. **Ad** alanına kasayı tanımlamak için kolay bir ad girin.
5. **Bölge** içinde, kasa için coğrafi bölgeyi seçin. Desteklenen bölgeleri kontrol etmek için bkz: [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
6. **Kasa Oluştur**'a tıklayın.
    ![Kasa oluşturma](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Kasanın başarıyla oluşturulduğunu doğrulamak için durum çubuğunu kontrol edin. Kasa olarak listelenen **etkin** ana **kurtarma Hizmetleri** sayfası.

## <a name="step-2-set-up-an-azure-network"></a>2. adım: Bir Azure ağı ayarlama
Azure ağı ayarlama, böylece Azure Vm'lerinin yük devretme sonrasında bir ağa bağlanacak ve şirket içi siteye geri dönme beklendiği gibi çalışabilmeniz için ayarlayın.

1. Azure portalında seçin **sanal ağ oluştur** ve ağ adı, IP adresi aralığı ve alt ağ adı belirtin.
2. Yeniden çalışma gerçekleştirmeniz gerekiyorsa, VPN/ExpressRoute ağ ekleyin. VPN/ExpressRoute bile yük devretme sonrasında ağa eklenebilir.

Azure ağlar hakkında daha fazla bilgi için bkz: [sanal ağlara genel bakış](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> Site Recovery dağıtımında kullanılan ağlar için aynı abonelik içindeki kaynak grupları arasında veya abonelik arasında [ağ geçişi](../azure-resource-manager/resource-group-move-resources.md) desteklenmez.
>
>

## <a name="step-3-install-the-vmware-components"></a>3. adım: VMware bileşenlerini yükleme
VMware sanal makineleri çoğaltmak istiyorsanız, yönetim sunucusunda aşağıdaki adımları izleyin:

1. [Karşıdan](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) ve VMware vSphere Powerclı 6.0 yükleyin.
2. Sunucuyu yeniden başlatın.

## <a name="step-4-download-a-vault-registration-key"></a>4. adım: kasa kayıt anahtarını indirin
1. Yönetim sunucusundan Azure Site kurtarma konsolunu açın. Üzerinde **kurtarma Hizmetleri** açmak için kasaya tıklayın **Hızlı Başlangıç** sayfası. Ayrıca açabilirsiniz **Hızlı Başlangıç** simgeyi tıklatarak herhangi bir zamanda sayfası.

    ![Hızlı Başlangıç simgesi](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Üzerinde **Hızlı Başlangıç** sayfasında, **hazırlama hedef kaynaklar** > **bir kayıt anahtarı indirin**. Kayıt dosyası otomatik olarak oluşturulur. Oluşturulduktan sonra beş gün boyunca geçerli değil.

## <a name="step-5-install-the-management-server"></a>5. adım: Yönetim sunucusu yükleme
> [!TIP]
> Bu URL'leri yönetim sunucusundan erişilebilir olduğundan emin olun:
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



1. Üzerinde **Hızlı Başlangıç** sayfasında, sunucuya birleşik yükleme dosyasını indirin.
2. Kurulum'u başlatmak için yükleme dosyasını çalıştırın **Site Recovery birleşik Kurulumu** Sihirbazı.
3. **Başlamadan önce** bölümünde **Yapılandırma sunucusu ve işlem sunucusunu yükle**’yi seçin.

   ![Başlamadan önce](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. İçinde **üçüncü taraf yazılım lisansı**, tıklatın **kabul ediyorum** indirmek ve MySQL yüklemek için.

    ![Üçüncü taraf yazılım](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. İçinde **kayıt**göz atın ve kasadan indirdiğiniz kayıt anahtarı seçin.

    ![Kayıt](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. İçinde **Internet ayarlarını**, yapılandırma sunucusunda çalışan sağlayıcı Internet üzerinden Azure Site Recovery hizmetine nasıl bağlanacağını belirleyin.

   * O anda makine üzerinde ayarlanmış olan bir ara sunucu ile bağlanmak isterseniz **Var olan ara sunucu ayarlarıyla bağlan** seçeneğini belirleyin.
   * Sağlayıcı doğrudan bağlanmasını istiyorsanız seçin **bir proxy sunucu olmadan doğrudan bağlan**.
   * Mevcut proxy kimlik doğrulaması gerektiriyorsa veya özel bir ara sunucu sağlayıcısı bağlantılarında kullanmak istiyorsanız, **özel proxy ayarlarıyla Bağlan**.
     * Özel bir ara sunucu kullanırsanız adresi, bağlantı noktası ve kimlik bilgilerini belirtmeniz gerekir.
     * Bir proxy sunucu kullanıyorsanız, zaten aşağıdaki URL'lere izin:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Güvenlik duvarı](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. İçinde **Önkoşul denetimi**, Kur'u çalıştıran yükleme çalışabildiğinden emin olmak için kontrol edin.

    ![Ön koşullar](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     **Genel saat eşitleme denetimi** hakkında bir uyarı görünürse, sistem saatindeki zamanın (**Tarih ve Saat** ayarları) saat dilimiyle aynı olduğunu doğrulayın.

     ![Zaman eşitleme sorunu](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. İçinde **MySQL yapılandırma**, yüklenecek MySQL server örneğine oturum açmak için kimlik bilgileri oluşturun.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. **Ortam Ayrıntıları**’nda VMware sanal makinelerini çoğaltıp çoğaltmayacağınızı seçin. Varsa, Kurulum Powerclı 6.0 yüklü olduğunu denetler.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. **Yükleme Konumu** alanında ikili dosyaları yüklemek ve önbelleği depolamak istediğiniz konumu seçin. En az 5 GB kullanılabilir disk alanı olan bir sürücü seçebilirsiniz, ancak en az 600 GB kullanılabilir disk alanı olan bir önbellek sürücüsü kullanmanızı öneririz.

   ![Yükleme konumu](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. İçinde **Ağ Seçimi**, üzerinde yapılandırma sunucusuna gönderir ve çoğaltma verilerini alma dinleyicisini (ağ bağdaştırıcısı ve SSL bağlantı noktası) belirtin. Varsayılan değiştirebilirsiniz (9443) bağlantı noktası. Bu bağlantı noktası ek olarak, bağlantı noktası 443'ü çoğaltma işlemlerini düzenler bir web sunucusu tarafından kullanılır. 443 çoğaltma trafiğini almak için kullanmayın.

    ![Ağ seçimi](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. **Özet** alanındaki bilgileri gözden geçirin ve **Yükle**’ye tıklayın. Yükleme tamamlandığında bir parola oluşturulur. Çoğaltmayı etkinleştirmek, bu nedenle onu kopyalayın ve güvenli bir konumda saklayın olduğunda bu anahtar gerekir.

   ![Özet](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Microsoft Azure kurtarma hizmeti Aracısı proxy ayarlanması gerekir.
> Yükleme tamamlandıktan sonra Microsoft Azure kurtarma Hizmetleri Kabuğu Windows Başlat menüsünden başlatın. Açılan komut penceresinde komutlar proxy sunucusu ayarlarını ayarlamak için aşağıdaki kümesini çalıştırın.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-the-command-line"></a>Kurulum komut satırından çalıştırma
Ayrıca birleşik Sihirbazı'nı komut satırından aşağıdaki gibi çalıştırabilirsiniz:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]

Konumlar:

* /ServerMode: Zorunlu. Yükleme yapılandırma ve işlem sunucuları veya yalnızca işlem sunucusu yükleyip yüklemeyeceğini belirtir (ek işlem sunucuları yüklemek için kullanılır). Giriş değerleri: CS, PS.
* InstallDrive: zorunlu. Bileşenlerinin yüklendiği klasörü belirtir.
* / MySQLCredFilePath. Zorunlu. MySQL server kimlik bilgilerinin depolandığı bir dosyanın yolunu belirtir. Dosyası oluşturmak için Şablon Al.
* / VaultCredFilePath. Zorunlu. Kasa kimlik bilgileri dosyası konumu.
* /EnvType. Zorunlu. Yükleme türü. Değerler: VMware, NonVMware.
* /PSIP ve /CSIP. Zorunlu. İşlem sunucusu ve yapılandırma sunucusu IP adresi.
* /PassphraseFilePath. Zorunlu. Parola dosyasının konumu.
* / ByPassProxy. İsteğe bağlı. Ara sunucu olmadan Azure'a bağlanır yönetim sunucusunu belirtir.
* /ProxySettingsFilePath. İsteğe bağlı. (Varsayılan proxy sunucusunda kimlik doğrulaması gerektirir) ya da özel proxy özel bir ara sunucu ayarlarını belirtir.

## <a name="step-6-set-up-credentials-for-the-vcenter-server"></a>6. adım: vCenter sunucusu için kimlik bilgilerini ayarlayın
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

İşlem sunucusu VMware vCenter sunucusu tarafından yönetilen sanal makineleri otomatik olarak bulabilir. Otomatik bulma için Site Recovery, bir hesap ve vCenter sunucusu erişmek için kimlik bilgileri gerekir. Bu, yalnızca fiziksel sunucuları çoğaltıyorsanız ilgili değildir.

Hesap ve kimlik bilgilerini ayarlamak için:

1. VCenter sunucusu üzerinde bir rol oluşturmak (**Azure_Site_Recovery**) ile vCenter düzeyinde [gerekli izinleri](#vmware-permissions-for-vcenter-access).
2. Ata **Azure_Site_Recovery** vCenter kullanıcıya rol.

   > [!NOTE]
   > Salt okunur rolüne sahip bir vCenter kullanıcı hesabı, korumalı kaynak makinelerden kapatmadan yük devretme çalıştırabilirsiniz. Bu makineleri kapatmayı istiyorsanız, Azure_Site_Recovery rol gerekir. Yalnızca VM'ler VMware Azure'a geçiş ve geri dönecek gerekmez, salt okunur rol yeterli olur.
   >
   >
3. Hesap eklemek için **cspsconfigtool**. Masaüstünde kısayol olarak kullanılabilir ve bulunduğu onu [yükleme konumu] \home\svsystems\bin klasöründe bulunur.
4. **Hesapları Yönet** sekmesinde **Hesap Ekle**’ye tıklayın.

    ![Hesap ekleme](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. İçinde **hesap ayrıntıları**, vCenter sunucusuna erişmek için kullanılan kimlik bilgilerini ekleyin. Hesap adı Portalı'nda görünmesi için 15 dakikadan uzun sürebilir. Hemen güncelleştirmek için **yenileme** üzerinde **yapılandırma sunucularına** sekmesi.

    ![Ayrıntılar](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>7. adım: vCenter sunucuları ve ESXi konakları ekleme
VMware sanal makinelerini çoğaltıyorsanız bir vCenter sunucusu (veya ESXi ana bilgisayar) eklemeniz gerekir.

1. Üzerinde **sunucuları** > **yapılandırma sunucularına** sekmesine **vCenter Sunucusu Ekle**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. VCenter sunucusu veya ESXi ana bilgisayar ayrıntıları, önceki adımda vCenter server ve VMware vCenter server tarafından yönetilen sanal makineleri keşfetmek için kullanılan işlem sunucusu erişmek için belirtilen hesap adını ekleyin. VCenter sunucusu veya ESXi ana bilgisayar işlem sunucusu yüklü olduğu sunucuda aynı ağda yer.

   > [!NOTE]
   > VCenter sunucusu veya vCenter veya ana bilgisayar sunucusunda yönetici ayrıcalıklarına sahip olmayan bir hesapla ESXi konak ekliyorsanız, vCenter emin olun veya ESXi hesapları etkin bu ayrıcalıklarına sahip: Dağıtılmış Datacenter, veri deposu, klasör, Jost, ağ, kaynak, sanal makine ve vSphere geçin. VCenter sunucusunun etkin depolama görünümleri ayrıcalık gerekiyor.
   >
   >

    ![VCenter server ekleme](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Bulma tamamlandıktan sonra vCenter sunucusu listelenir **yapılandırma sunucularına** sekmesi.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>8. adım: bir koruma grubu oluşturma
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Koruma, sanal makine ya da aynı koruma ayarlarını kullanarak korumak istediğiniz fiziksel sunucuları mantıksal gruplandırmalarını gruplarıdır. Bir koruma grubu için koruma ayarları uygulamak ve bu ayarları gruba eklediğiniz tüm makineleri (sanal veya fiziksel) uygulanır.

1. Git **korunan öğeler** > **koruma grubu** ve bir koruma grubu eklemek için simgeyi tıklatın.

    ![Koruma grubu oluşturma](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Üzerinde **koruma grubu ayarlarını belirtin** sayfasında, grup için bir ad belirtin. İçinde **gelen** aşağı açılan listesinde, grubu oluşturmak istediğiniz yapılandırma sunucusunu seçin. **Hedef** Microsoft Azure.

    ![Koruma grubu ayarları](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Üzerinde **çoğaltma ayarlarını belirt** sayfasında, gruptaki tüm makineler için kullanılan çoğaltma ayarlarını yapılandırın.

    ![Koruma grubunun çoğaltma](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Çoklu VM tutarlılığı**: bunu açmanızı, paylaşılan uygulamaları tutarlı kurtarma noktaları koruma grubundaki makinelerde oluşturur. Koruma grubundaki tüm makinelerin aynı iş yükünü çalıştırırken bu en uygun bir ayardır. Tüm makineler aynı veri noktasına kurtarılır. VMware Vm'lerini veya fiziksel sunucular (Windows veya Linux) çoğaltma yapıyorsanız bu kullanılabilir.
   * **RPO eşiği**: RPO ayarlar. Sürekli veri koruma çoğaltma yapılandırılmış RPO eşik değerini aştığında uyarıları üretilir.
   * **Kurtarma noktası bekletme**: bekletme penceresi belirtir. Korumalı makineler, bu pencereyi içinde herhangi bir noktaya kurtarılabilir.
   * **Uygulamayla tutarlı anlık görüntü sıklığı**: uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktalarının ne sıklıkta oluşturulacak belirtir.

Onay işareti seçtiğinizde, belirttiğiniz ada sahip bir koruma grubu oluşturulur. Ayrıca, ikinci bir koruma grubu adıyla oluşturulur *koruma grubu adı*- yeniden çalışma. Azure'a yük devretme işleminden sonra şirket içi siteye başarısız olursa bu koruma grubu kullanılır. Oluşturulan koruma grupları izleyebilirsiniz **korunan öğeler** sayfası.

## <a name="step-9-install-the-mobility-service"></a>9. adım: mobilite hizmeti yükleme
Sanal makineler ve fiziksel sunucuları için korumayı etkinleştirmenin ilk adımı, Mobility hizmetini yüklemektir. Bunu iki şekilde yapabilirsiniz:

* Otomatik olarak anında ve işlem sunucusundan her makinede hizmetini yükleyin. Bir koruma grubu için makineleri ekleyin ve bunlar Mobility hizmeti uygun bir sürümünü çalıştırıyorsanız, anında yükleme karşılaşılmaz. Hizmet WSUS veya System Center Configuration Manager gibi Kurumsal gönderme yöntemini kullanarak da otomatik olarak yükleyebilirsiniz. Bunu yapmadan önce yönetimi sunucusunu ayarlama ayarladığınızdan emin olun.
* Hizmet, korumak istediğiniz her makinede el ile yükleyin. Bunu yapmadan önce yönetimi sunucusunu ayarlama ayarladığınızdan emin olun.

### <a name="install-the-mobility-service-with-push-installation"></a>Mobilite hizmetinin göndermeli yüklemesi ile yüklenmek
Bir koruma grubuna makineler eklediğinizde, Mobility hizmeti otomatik olarak gönderilir ve işlem sunucusu tarafından her makinede yüklü.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Windows makinelerinde otomatik gönderim için hazırlanma
Böylece mobilite hizmeti işlem sunucusu tarafından otomatik olarak yüklenebilmesi için Windows makineler hazırlamak için:

1. İşlem sunucusu makine erişmek için kullanabileceğiniz bir hesap oluşturun. Hesap (yerel veya etki alanı) yönetici ayrıcalıklarına sahip. Bu kimlik bilgileri yalnızca mobilite hizmetinin göndermeli yüklemesi için kullanılır.

   > [!NOTE]
   > Bir etki alanı hesabı kullanmıyorsanız, yerel makinede uzak kullanıcı erişim denetimi devre dışı bırakmanız gerekir. Bunu, kayıt defterinde HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System altında DWORD girişi LocalAccountTokenFilterPolicy değerinin 1 ile eklemek için altında. CLI açık komutundan veya PowerShell'i kullanarak kayıt defteri girdisini eklemek için şunu girin  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Korumak istediğiniz makinede Windows Güvenlik Duvarı için seçin **bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin**ve etkinleştirme **dosya ve Yazıcı Paylaşımı** ve **Windows Yönetim Araçları**. Bir etki alanına ait makineler için bir GPO ile güvenlik duvarı ilkesi yapılandırabilirsiniz.

   ![Güvenlik duvarı ayarları](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Oluşturduğunuz hesabı ekleyin:

   * **Cspsconfigtool**’u açın. Masaüstünde kısayol olarak kullanılabilir ve bulunduğu onu [yükleme konumu] \home\svsystems\bin klasöründe bulunur.
   * **Hesapları Yönet** sekmesinde **Hesap Ekle**’ye tıklayın.
   * Oluşturduğunuz hesabı ekleyin. Hesabını ekledikten sonra bir koruma grubu için bir makine eklediğinizde, kimlik bilgilerini sağlamanız gerekir.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Linux sunucularında otomatik gönderim için hazırlanma
1. Korumak istediğiniz Linux makine açıklandığı gibi desteklendiğinden emin olun [şirket içi Önkoşullar](#on-premises-prerequisites). Korumak istediğiniz makine ve işlem sunucusu çalıştıran yönetim sunucusu arasında ağ bağlantısı olduğundan emin olun.
2. İşlem sunucusu makine erişmek için kullanabileceğiniz bir hesap oluşturun. Kaynak Linux sunucusunda bir kök kullanıcı hesabı olmalıdır. Bu kimlik bilgileri yalnızca mobilite hizmetinin göndermeli yüklemesi için kullanılır.

   * **Cspsconfigtool**’u açın. Masaüstünde kısayol olarak kullanılabilir ve bulunduğu onu [yükleme konumu] \home\svsystems\bin klasöründe bulunur.
   * **Hesapları Yönet** sekmesinde **Hesap Ekle**’ye tıklayın.
   * Oluşturduğunuz hesabı ekleyin. Hesabını ekledikten sonra bir koruma grubu için bir makine eklediğinizde, kimlik bilgilerini sağlamanız gerekir.
3. Kaynak Linux sunucusundaki /etc/hosts dosyasında, yerel ana bilgisayar adını tüm ağ bağdaştırıcıları ile ilişkili IP adreslerine eşleyen girişler olduğunu denetleyin.
4. En son openssh, openssh sunuculu ve openssl paketleri korumak istediğiniz makineye yükleyin.
5. SSH bağlantı noktası 22 etkin ve çalışıyor olduğundan emin olun.
6. SFTP alt sistemi ve parola ile kimlik doğrulamasını sshd_config dosyasında aşağıdaki gibi etkinleştirin:

   * Kök olarak oturum açın.
   * /Etc/ssh/sshd_config dosyasında PasswordAuthentication ile başlayan satırı bulun.
   * Satırı açıklama durumundan çıkarın ve değerini **no (hayır)** yerine **yes (evet)** olarak değiştirin.
   * **Subsystem** ile başlayan satırı bulun ve açıklama durumundan çıkarın.

     ![Linux hiçbir alt sistemlerin varsayılan geçersiz kılma](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-the-mobility-service-manually"></a>Mobility hizmeti el ile yükleyin
C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository yükleyicileri kullanılabilir.

| Kaynak işletim sistemi | Mobility hizmeti yükleme dosyası |
| --- | --- |
| Windows Server (yalnızca 64 bit) |Microsoft-ASR_UA_9*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (yalnızca 64 bit) |Microsoft-ASR_UA_9*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (yalnızca 64 bit) |Microsoft-ASR_UA_9*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (yalnızca 64 bit) |Microsoft-ASR_UA_9*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-the-mobility-service-manually-on-a-windows-server"></a>Mobility hizmeti el ile bir Windows sunucusuna yükleyin
1. İlgili yükleyiciyi indirip çalıştırın.
2. **Başlamadan önce** bölümünde **Mobility hizmeti**’ni seçin.

    ![Mobility hizmeti yüklemesi](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. İçinde **yapılandırma sunucusu ayrıntılarını**, yönetim sunucusu ve yönetim sunucusu bileşeni yüklü olduğunda oluşturulan parolayı IP adresini belirtin. Çalıştırarak parola alabilir  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** yönetim sunucusunda.

    ![Mobility hizmeti](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. İçinde **yükleme konumu**, varsayılan Konum'u tutabilir ve tıklayın **sonraki** yüklemeyi başlatmak için.
5. İçinde **yükleme ilerleme durumu**, yükleme kontrol edin ve istenirse makineyi yeniden başlatın.

Ayrıca, aşağıdaki komut satırını metin girerek yükleyebilirsiniz:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

Önceki komutta:

* / Rol: zorunlu. Mobility hizmetinin yüklenmesinin gerekip gerekmediğini belirtir.
* / Installlocation: zorunlu. Hizmetin yükleneceği konumu belirtir.
* / PassphraseFilePath: zorunlu. Yapılandırma sunucusunun parolası belirtir.
* / LogFilePath'i: zorunlu. Günlük kurulum dosyası konumu belirtir.

#### <a name="uninstall-the-mobility-service-manually"></a>Mobility Hizmetini el ile kaldırma
Mobility hizmeti kullanarak kaldırabilirsiniz **Kaldır veya Değiştir bir program** Denetim Masası'nda veya komut satırını kullanarak.

Komut satırını kullanarak Mobility hizmetini kaldırmak için bir komut şöyledir:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-the-ip-address-of-the-management-server"></a>Yönetim sunucusunun IP adresini değiştirme
Sonra sihirbazı çalıştırın, yönetim sunucusunun IP adresini aşağıdaki gibi değiştirebilirsiniz:

1. Dosya hostconfig.exe (masaüstünde bulunur) açın.
2. Üzerinde **genel** sekmesinde, yönetim sunucusunun IP adresini değiştirin.

   > [!NOTE]
   > Yalnızca yönetim sunucusunun IP adresini değiştirin. Yönetim sunucu iletişimi için bağlantı noktası numarası 443 olmalıdır ve **HTTPS kullan** sol etkinleştirilmesi gerekir. Parolayı değiştirmeyin.
   >
   >

    ![Yönetim sunucusu IP adresi](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-the-mobility-service-manually-on-a-linux-server"></a>Mobility hizmetinin Linux sunucusu üzerinde el ile yükleyin.
1. Uygun tar arşiv korumak istediğiniz Linux bilgisayara kopyalayın. Altındaki tabloya bakın [Mobility hizmeti el ile yüklemek](#install-the-mobility-service-manually) belirlemek için hangi tar arşiv kullanmanız gerekir.
2. Bir kabuk programı açmak ve bir yerel yol daraltılmış tar arşive çalıştırarak ayıklayın:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Tar arşiv içeriğini ayıkladığınız yerel dizindeki passphrase.txt adlı bir dosya oluşturun. Bunu yapmak için parolayı C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase yönetim sunucusuna kopyalayın ve çalıştırarak içinde passphrase.txt kaydetmek  *`echo <passphrase> >passphrase.txt`*  Kabuğu'nda.
4. Mobility hizmeti, aşağıdaki komutu girerek yükleyin:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Yönetim sunucusunun iç IP adresi belirtin ve 443 numaralı bağlantı noktasını seçili olduğundan emin olun.

#### <a name="install-the-mobility-service-from-the-command-line"></a>Komut satırından Mobility hizmetini yükleme

Yönetim sunucusunda C:\Program Files (x86) \InMage Systems\private\connection parolayı kopyalayın ve yönetim sunucusu üzerindeki "passphrase.txt" kaydedin. Ardından aşağıdaki komutları çalıştırın. Örneğimizde, yönetim sunucusu IP adresi 104.40.75.37 ve HTTPS bağlantı noktası 443'tür:

Bir üretim sunucusuna yüklemek için:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

Ana hedef sunucuya yüklemek için:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>10. adım: bir makine için korumayı etkinleştirin
Korumayı etkinleştirmek için sanal makineleri ve fiziksel sunucuları bir koruma grubuna ekleyin. Başlamadan önce VMware sanal makineleri koruyorsanız aşağıdakileri unutmayın:

* VMware Vm'lerini her 15 dakikada bulunan ve bunları bulmadan sonra Site kurtarma Portalı'nda görünmesi için 15 dakikadan uzun sürebilir.
* Ortam değişiklikleri (örneğin, VMware araçları yükleme) sanal makinedeki ayrıca Site Recovery güncelleştirilmesi için birden fazla 15 dakika sürebilir.
* VMware Vm'leri için son keşfedilen zamanı denetleyebilirsiniz **en son kişi** üzerinde vCenter sunucusu/ESXi ana bilgisayar için alan **yapılandırma sunucularına** sekmesi.
* Bir koruma grubu oluşturduktan sonra bir vCenter sunucusu veya ESXi ana bilgisayar eklerseniz, 15 dakikadan fazla yer alması için sanal makineler ve yenilemek Azure Site Recovery portalı için sürebilir **makineleri bir koruma grubuna eklemek** iletişim kutusu.
* İşleme devam etmek ve zamanlanmış bulma beklemeden bir koruma grubu için makineleri eklemek istiyorsanız, yapılandırma sunucusu vurgulayın (tıklatın yok) tıklatıp **yenileme**.

Buna ek olarak:

* Böylece, iş yüklerini yansıtma koruma gruplarınızı mimari öneririz. Örneğin, aynı gruba belirli bir uygulama çalışan makineleri ekleyin.
* Bir koruma grubuna makineler eklediğinizde, işlem sunucusu otomatik olarak iter ve zaten yüklü değilse Mobility hizmetini yükler. Önceki adımda açıklanan şekilde hazırlanmış itme mekanizması sahip olmanız gerekir.

### <a name="add-machines-to-a-protection-group"></a>Bir koruma grubu için makineleri ekleyin

1. Git **korunan öğeleri** > **koruma grubu** > **makineler** > **makineleri ekleyin**.
2. VMware sanal makineleri koruyorsanız **sanal makineleri seçin**, sanal makinelerinizi (veya bunlar çalışmakta olduğu EXSi konak) yönetme bir vCenter sunucusu seçin ve ardından makineleri seçin.

    ![Sanal makineler için korumayı etkinleştir](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. İçinde fiziksel sunucuları koruyorsanız **sanal makineleri seçin**, açık **eklemek fiziksel makineleri** Sihirbazı'nı ve IP adresi ve kolay bir ad sağlayın. Ardından işletim sistemi ailesi seçin.

   ![Fiziksel sunucuları için korumayı etkinleştirin](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. İçinde **belirtin hedef kaynaklar**, çoğaltma için kullandığınız depolama hesabını seçin ve ayarları tüm iş yükleri için kullanılması gereken olup olmadığını seçin. Premium depolama hesapları şu anda desteklenmiyor.

   > [!NOTE]
   > Taşıma depolama hesapları kullanılarak oluşturulan desteklemiyoruz [Azure portal](../storage/storage-create-storage-account.md) kaynak grupları arasında.                           
   > Site Recovery dağıtımında kullanılan depolama hesapları için aynı abonelik içindeki kaynak grupları arasında veya abonelik arasında [depolama hesapları geçişi](../azure-resource-manager/resource-group-move-resources.md) desteklenmez.
   >
   >

    ![Hedef ayarlarını yapılandırma](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. İçinde **belirtin hesapları**, hesabı seçin, [ayarlamak](#install-the-mobility-service-with-push-installation) otomatik mobilite hizmetinin yüklenmesi için kullanılacak.

    ![Hesaplarını belirtin](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Makineleri koruma grubuna eklemeyi bitirdikten ve her makine için ilk çoğaltmayı başlatmak için onay işaretine tıklayın.

   > [!NOTE]
   > Yükleme hazırlandı, Mobility hizmeti, koruma grubuna eklenen sahip makinelerde otomatik olarak yüklenir. Hizmeti yüklendikten sonra bir koruma işi başlatır ve başarısız olur. Hatadan sonra Mobility hizmeti yüklenmiş olan her makineye el ile yeniden başlatmanız gerekir. Yeniden başlatma işleminden sonra koruma işini yeniden başlar ve ilk çoğaltma gerçekleştirilir.
   >
   >

Durumunu izleyebilirsiniz **işleri** sayfası.

![İşlerini sayfasında durumunu izleyin](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

Koruma durumunu da izlenebilir içinde **korunan öğeler** > *koruma grubu adı* > **sanal makineleri**. İlk çoğaltma sonlandırıldıktan sonra verileri eşitlenir, makine durumu değişikliklerini **korumalı**.

![Korumalı öğeleri durumunu izleyin](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>11. adım: Korunan kümesi makine özellikleri
1. Bir makine sahip olduktan sonra bir **korumalı** durumu, yük devretme özelliklerini yapılandırabilirsiniz. Koruma grubu ayrıntıları makine seçin ve açın **yapılandırma** sekmesi.
2. Site Recovery otomatik olarak Azure VM için özellikler önerir ve şirket içi ağ ayarlarını algılar.

    ![Sanal makine özelliklerini ayarla](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. Bu ayarları değiştirebilirsiniz:

   * **Azure VM adı**: Bu yük devretme sonrasında Azure makineye verilecek addır. Ad, Azure gereksinimlere uygun olmalıdır.
   * **Azure VM boyutu**: için hedef sanal makine belirtin, ağ bağdaştırıcılarının sayısını boyuta göre dikte edilir. Boyutları ve bağdaştırıcılar hakkında daha fazla bilgi için bkz: [boyut tabloları](../virtual-machines/linux/sizes.md). Şunlara dikkat edin:

     * Bir sanal makine boyutunu değiştirme ve ayarları kaydettiğinizde, açtığınızda, ağ bağdaştırıcısı sayısı değişir **yapılandırma** sekmesinde sonraki. Hedef sanal makinelerin ağ bağdaştırıcılarında en az sayıda kaynak sanal makinedeki ağ bağdaştırıcıları en az sayıda eşittir. Ağ bağdaştırıcısı sayısı, sanal makine boyutu tarafından belirlenir.
       * Kaynak makinedeki ağ bağdaştırıcıları sayısı, hedef makine boyutu için izin verilen bağdaştırıcıları sayısına eşit veya daha az ise, hedef kaynak olarak aynı sayıda bağdaştırıcıya sahip.
       * Kaynak sanal makinenin bağdaştırıcı sayısı hedef boyutu için izin verilen sayıyı aşarsa maksimum hedef boyutu kullanılır.
        Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hedef makinenin iki bağdaştırıcısı olur. Kaynak makinenin iki bağdaştırıcısı varken hedef boyut yalnızca bir destekler, hedef makine yalnızca bir bağdaştırıcısı olur.
     * Sanal makinede birden fazla ağ bağdaştırıcısı varsa, tüm bağdaştırıcıları aynı Azure ağa bağlanması gerekir.
   * **Azure ağı**: Azure Vm'lerinin yük devretme sonrasında bağlanacağı bir Azure ağı belirtmeniz gerekir. Bir belirtmezseniz, Azure sanal makinelerini herhangi bir ağa bağlanmayacaktır. Ayrıca, şirket içi siteye Azure'dan yeniden çalışma için istiyorsanız bir Azure ağı belirtmeniz gerekir. Yeniden çalışma bir Azure ağı ve bir şirket ağı arasında bir VPN bağlantısı gerektirir.
   * **Azure IP adresi/alt ağı**: her ağ bağdaştırıcısı için olduğu Azure VM bağlanmak alt ağ seçin. Kaynak makinenin ağ bağdaştırıcısı statik bir IP adresi kullanmak üzere yapılandırılmışsa, bir statik IP adresi için Azure VM belirtebilirsiniz unutmayın. Statik bir IP adresi sağlamazsanız, herhangi bir kullanılabilir IP adresi ayrılır. Hedef IP adresi belirtildiğinden, ancak bunu Azure başka bir VM tarafından kullanılıyor, yük devretme başarısız olur. Kaynak makinenin ağ bağdaştırıcısı, DHCP kullanmak üzere yapılandırılmışsa, Azure ayarı olarak DHCP sahip olacaksınız.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>12. adım: bir kurtarma planı oluşturma ve yük devretme gerçekleştirme
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

Aynı görevi gerçekleştirmek ya da aynı iş yükünü çalıştırmak birden çok sanal makine üzerinde başarısız olabilir veya tek bir makine için yük devretme çalıştırabilirsiniz. Aynı anda birden fazla makine üzerine vermesine, bunları bir kurtarma planına ekleyin.

Bir kurtarma planı oluşturmak için:

1. Üzerinde **kurtarma planları** sayfasında, **eklemek kurtarma planı** ve bir kurtarma planı ekleyin. Seçin ve planı için ayrıntıları belirtin **Azure** hedefi olarak.

 ![Kurtarma planı yapılandırın](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. İçinde **sanal makineyi Seç**, bir koruma grubu seçin ve kurtarma planına eklenecek grubundaki makineleri seçin.

 ![Sanal makineleri ekleyin](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

Grupları ve sıra içinde makineler kurtarma planında yük devredildi sipariş oluşturmak için plan özelleştirebilirsiniz. Komut dosyaları ve el ile gerçekleştirilen eylemleri için ister de ekleyebilirsiniz. Komut dosyaları el ile veya kullanılarak oluşturulabilir [Azure Automation Runbook](site-recovery-runbook-automation.md). Kurtarma planları özelleştirme hakkında daha fazla bilgi için bkz: [kurtarma planları oluşturabilirsiniz](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Yük devretme gerçekleştirme
Bir yük devretme çalıştırmadan önce:

* Yönetim sunucusu çalışır ve kullanılabilir olduğundan emin olun. Değilse, yük devretme başarısız olur.
* Planlanmamış bir yük devretme çalıştırırsanız:

  * Mümkün olduğu durumlarda, planlanmamış bir yük devretmeyi çalıştırmadan önce birincil makineleri kapatmanız gerekir. Bu işlem, kaynak ve çoğaltılan makinelerin aynı anda çalışmamasını garantiler. Planlanmamış bir yük devretme çalıştırdığınızda, VMware sanal makinelerini çoğaltıyorsanız Site Recovery kaynak makineleri kapatmayı denemelisiniz belirtebilirsiniz. Birincil site durumunu, bağlı olarak bu olabilir veya çalışmayabilir. Fiziksel sunucuları çoğaltma yapıyorsanız Site Recovery bu seçeneği sağlamaz.
  * Planlanmamış bir yük devretme birincil makinelerden veri çoğaltma durur, böylece planlanmamış bir yük devretme başladıktan sonra hiçbir veri değişim aktarılan olmaz.
  * Yük devretme sonrasında Azure içinde çoğaltma sanal makinesine bağlanmak isterseniz yük devretme çalıştırmadan önce kaynak makinede Uzak Masaüstü Bağlantısı etkinleştirin. Ardından RDP bağlantısı güvenlik duvarı aracılığıyla izin verin. Yük devretme sonrasında Azure sanal makinesini ortak uç nokta RDP izni gerekir. İzleyin [en iyi uygulamalar](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) RDP yük devretme sonrasında çalıştığından emin olmak için.

> [!NOTE]
> Azure'a yük devretme yaptığınızda en iyi performansı elde etmek için korunan makineye Azure Aracısı'nı yüklediğinizden emin olun. Bu makine önyükleme daha hızlı yardımcı olur ve sorunları tanılamanıza yardımcı olur. Azure Aracısı'nı kullanılabilir [Linux](https://github.com/Azure/WALinuxAgent) ve [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
Yük devretme testi, yük devretme benzetimi için çalıştırın ve kurtarma işlemleri, üretim ortamınızın etkilemez ve normal çoğaltma olanak tanır yalıtılmış bir ağda normal olarak devam edin. Yük devretme testi initiatd kaynağı olan ve birkaç yolla içinde çalıştırın:

* **Bir Azure ağı belirtmeyin**: yük devretme testi ağ olmadan çalıştırırsanız, test sanal makineleri başlatın ve doğru Azure'da görünmesi kontrol eder. Sanal makineler, yük devretme sonrasında Azure bir ağa bağlanmayacaktır.
* **Bir Azure ağı belirtin**: Bu tür bir yük devretme tüm çoğaltma ortamının istendiği şekilde geldiğini ve Azure sanal makineleri belirtilen ağa bağlı olduğunu denetler.

Yük devretme testi çalıştırmak için:

1. Üzerinde **kurtarma planları** sayfasında planı seçin ve tıklayın **yük devretme testi**.

 ![Planı seçin](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. İçinde **sınama yük devretmesi onaylayın**seçin **hiçbiri** yük devretme sınaması için bir Azure ağı kullanmayı seçebilir veya için test sanal makineleri bağlı olacak yük devretme sonrasında ağ istemediğiniz belirtmek için. Yük devretmeyi başlatmak için onay işaretine tıklayın.

 ![Bir seçim yapın](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Yük devretme işleminin ilerleyişini izlemek **işleri** sekmesi.

 ![İlerlemeyi izleme](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Yük devretme işlemi tamamlandıktan sonra da Azure çoğaltma görüyor olmalısınız makine görünür **sanal makineleri** Azure portalında. Azure VM için RDP bağlantısı başlatmak istiyorsanız, VM uç 3389 numaralı bağlantı noktasını açın gerekir.
5. Sonra tamamlanmış, yük devretme ulaştığında **tam** aşaması, test tıklatın **tam Test** tamamlamak için. İçinde **notları**, kaydetme ve yük devretme testiyle ilişkili gözlemlerinizi kaydetmek.
6. Tıklatın **test yük devretmesi tamamlandıktan** otomatik olarak test ortamını temizleyin. Bu yapıldıktan sonra Yük devretme sınaması gösterecektir bir **tam** durumu. Tüm öğeler ve yük devretme testi sırasında otomatik olarak oluşturulan VM'ler silinir. Yük devretme testi iki haftadan fazla sürerse tamamlanması gerektirdi.

### <a name="run-an-unplanned-failover"></a>Planlanmamış bir yük devretmeyi çalıştırma
Planlanmamış yük devretme Azure'dan başlatılır ve birincil site kullanılamıyorsa bile gerçekleştirilebilir.

1. Üzerinde **kurtarma planları** sayfasında planı seçin ve tıklayın **yük devretme** > **planlanmamış yük devretme**.

 ![Planı seçin](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. VMware sanal makinelerini çoğaltıyorsanız şirket içi sanal makineleri kapatmayı deneyebilirsiniz. Bu en yüksek çaba bir eylemdir ve çaba veya başarılı olup olmadığını yük devretme devam eder. İşlemi başarılı değil, hata ayrıntıları görünür **işleri** altında sekmesinde **planlanmamış yük devretme işleri**.

 ![Şirket içi VM'ler kapatılıyor seçeneği](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Fiziksel sunucuları çoğaltma yapıyorsanız bu seçenek kullanılamaz. Bu el ile mümkünse kapatmak denemeniz gerekir.
 >
 >

3. İçinde **onaylayın yük devretme**, yük devretme yönü (Azure) emin olun ve yük devretme için kullanmak istediğiniz kurtarma noktasını seçin. Çoğaltma özelliklerini yapılandırıldığında çoklu VM etkinleştirilirse, en son uygulama veya kilitlenme tutarlı kurtarma noktası kurtarabilirsiniz. Öğesini de seçebilirsiniz **özel kurtarma noktası** zamandaki önceki bir noktaya kurtarmak için. Yük devretmeyi başlatmak için onay işaretine tıklayın.

 ![Yük devretme yönü onaylayın](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Planlanmamış yük devretme işinin bitmesini bekleyin. Yük devretme işleminin ilerleyişini izleyebilirsiniz **işleri** sekmesi. Planlanmamış yük devretme sırasında bir hata oluşmamasına olsa bile tamamlanıncaya kadar kurtarma planı çalıştırır. Ayrıca Azure çoğaltma görmeye olmalıdır makine görünür **sanal makineleri** Azure portalında.

### <a name="connect-to-replicated-azure-virtual-machines-after-failover"></a>Çoğaltılan Azure sanal makinelere yük devretme sonrasında bağlanmak
Çoğaltılmış sanal makinelere Azure yük devretme sonrasında bağlanmak için gerekir:

- Birincil makinede etkin bir Uzak Masaüstü Bağlantısı.
- Windows Güvenlik Duvarı birincil makinede RDP izin verecek şekilde ayarlayın.
- Genel bir uç nokta Azure sanal makinesi için RDP eklendi.

Bu ayarlama hakkında daha fazla bilgi için bkz: [ASR kullanarak yük devretme sonrasında Uzak Masaüstü bağlantı sorunlarını giderme](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="deploy-additional-process-servers"></a>Ek işlem sunucusu dağıtın
200 kaynak makinelerden ötesinde, dağıtımınızın ölçeğini gerekir ya da 2 TB toplam günlük karmaşıklık oranı aşarsa, trafik hacmi işlemek için ek işlem sunucuları gerekir. Bir ek işlem sunucusu kurmak için gereksinimleri iade etme [ek işlem sunucuları](#additional-process-servers)ve ardından aşağıdaki yönergelere göre işlem sunucusu ayarlayın. Sunucuyu ayarladıktan sonra kaynak makine kullanmak için yapılandırabilirsiniz.

### <a name="set-up-an-additional-process-server"></a>Bir ek işlem sunucusu kurma
Bir ek işlem sunucusu ayarlamadıysanız aşağıdaki gibi ayarlayın:

* Bir yönetim sunucusu yalnızca bir işlem sunucusu olarak yapılandırmak için birleşik sihirbazını çalıştırın.
* Veri çoğaltma yalnızca yeni işlem sunucusu kullanarak yönetmek istiyorsanız, korumalı makinelerinizi geçirmek gerekir.

### <a name="install-the-process-server"></a>İşlem sunucusu yükleyin
1. Üzerinde **Hızlı Başlangıç** sayfasında, Site Recovery bileşen yüklemesi birleşik yükleme dosyasını indirin. Kur'u yeniden çalıştırın.
2. **Başlamadan önce** kısmında **Dağıtımı genişletmek için ek işlem sunucuları ekleyin**’i seçin.

 ![İşlem sunucusu ekleme](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Ne zaman yaptığınız gibi Sihirbazı tamamlayın, [ayarlanan](#step-5-install-the-management-server) ilk yönetim sunucusu.
4. İçinde **yapılandırma sunucusu ayrıntılarını**yapılandırma sunucusu yüklediğiniz ilk yönetim sunucusunun IP adresini girin ve ardından parolayı girin. Parola yoksa çalıştırmak  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** bunu almak için özgün yönetim sunucusunda.

 ![Yapılandırma sunucusu ayrıntıları](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-to-use-the-new-process-server"></a>Yeni işlem sunucusu kullanabilmek için makineleri geçirin
1. Açık **yapılandırma sunucularına** > **Server** > *özgün yönetim sunucusu adını* > **sunucu ayrıntıları**.

 ![Sunucu Ayrıntıları](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. İçinde **işlem sunucuları** listesinde **işlem sunucusunu Değiştir** değiştirmek istediğiniz sunucunun yanındaki.

 ![İşlem sunucusu güncelleştir](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Seçin **işlem sunucusunu Değiştir**seçin **hedef işlem sunucusunu**ve ardından yeni yönetim sunucusu seçin. Ardından yeni işlem sunucusu işleyecek sanal makineleri seçin. Sunucu hakkında bilgi almak için bilgi simgesine tıklayın. Seçilen her sanal makine için yeni işlem sunucusu çoğaltmak için gerekli olan ortalama alanı kararları yük yapmanıza yardımcı olmak için görüntülenir. Yeni işlem sunucusu için çoğaltma başlatmak için onay işaretine tıklayın.

 ![İşlem sunucusunu değiştirme](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>VMware vCenter erişim izinlerini
İşlem sunucusu, bir vCenter sunucusu üzerinde sanal makineleri otomatik olarak bulabilir. Otomatik keşfi gerçekleştirmek için bir rol (Azure_Site_Recovery) tanımlamak vCenter sunucusuna erişmek Site Recovery izin vermek için vCenter düzeyinde gerekir. Yalnızca VMware makineleri Azure'a geçirmek ve gerekiyorsa Azure'dan yeniden çalışma için gereken, yeterli salt okunur bir rolü tanımlayabilirsiniz. Bölümünde açıklandığı gibi izinlerini ayarlama [adım 6: vCenter sunucusu için kimlik bilgilerini ayarlama](#step-6-set-up-credentials-for-the-vcenter-server). Rol izinleri aşağıdaki tabloda özetlenmiştir:

| **Rol** | **Ayrıntılar** | **İzinler** |
| --- | --- | --- |
| Azure_Site_Recovery rolü |VMware VM bulma |V merkezi sunucusu için şu ayrıcalıkları atayın:<br/><br/>Veri deposu: Tahsis alanı, Gözat veri deposu, alt düzey dosya işlemleri, dosya, güncelleştirme sanal makine dosyalarını Kaldır<br/><br/>Ağ: Ağ atama<br/><br/>Kaynak: sanal makine atama kaynak havuzu, sanal makine Gücü Kapat geçirme, sanal makine gücü açma geçirme<br/><br/>Görevler: görev, güncelleştirme görevi oluşturma<br/><br/>Sanal makine > yapılandırma<br/><br/>Sanal makine > etkileşimde bulunma > yanıt soru, cihaz bağlantısı, yapılandırma CD medyasından, yapılandırma disket ortamı, kapatma, açma, VMware araçları yükleme<br/><br/>Sanal makine > Stok > oluşturun, kayıt, kayıt Sil<br/><br/>Sanal makine > sağlama > izin sanal makine indirme, izin sanal makine dosyaları karşıya yükleme<br/><br/>Sanal makine > anlık görüntüleri > anlık görüntüleri kaldırma |
| vCenter kullanıcı rolü |VMware VM bulma/olmadan yük devretme kaynak VM kapatma |V merkezi sunucusu için şu ayrıcalıkları atayın:<br/><br/>Veri Merkezi nesnesi > Propagate alt nesne için rol = salt okunur <br/><br/>Kullanıcı veri merkezi düzeyinde atanır ve bu nedenle tüm nesneler veri merkezinde erişimi. Erişimi kısıtlamak istiyorsanız, Ata **erişim yok** rolüyle **alt Propagate** (ESX konakları, datastores, sanal makineleri ve ağları) alt nesneleri için nesne. |
| vCenter kullanıcı rolü |Yük devretme ve yeniden çalışma |V merkezi sunucusu için şu ayrıcalıkları atayın:<br/><br/>Veri Merkezi nesnesi – Propagate alt nesne için rol Azure_Site_Recovery =<br/><br/>Kullanıcı veri merkezi düzeyinde atanır ve bu nedenle tüm nesneler veri merkezinde erişimi.  Erişimi kısıtlamak istiyorsanız, Ata ** erişim yok ** rolüyle **Propagate alt nesne için** alt nesnesine (ESX konakları, datastores, sanal makineleri ve ağları). |

## <a name="third-party-software-notices-and-information"></a>Üçüncü taraf yazılım uyarılar ve bilgiler
<!--Do Not Translate or Localize-->

Microsoft ürünü veya hizmetinde çalışan bellenim ve yazılım dayanır veya malzeme aşağıda listelenen projelerden birleştirir (topluca "üçüncü taraf kodu").  Microsoft, üçüncü taraf kodu değil özgün yazarı almıştır.  Özgün telif hakkı bildirimi ve lisans altında Microsoft gibi üçüncü taraf kodu alındı, aşağıda belirtilen ayarlanır.

Bir bölümdeki bilgiler, aşağıda listelenen projelerden üçüncü taraf kodu bileşenleri ile ilgili. Bu tür lisansları ve bilgi yalnızca bilgilendirme amacıyla sağlanır.  Bu üçüncü taraf kodu size Microsoft tarafından Microsoft Ürün veya hizmet için Microsoft Yazılımı Lisans koşulları altında relicensed.  

Bölüm B bilgileri size Microsoft tarafından özgün lisans koşullarına sunulmaktadır üçüncü taraf kodu bileşenleri ilgili olduğu.

Tam dosya üzerinde bulunabilir [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft tarafından uygulanır olup olmadığını, belirtilmeyen tüm hakları ayırır rıza ya da aksi takdirde.

## <a name="next-steps"></a>Sonraki adımlar
[Yeniden çalışma hakkında daha fazla bilgi](site-recovery-failback-azure-to-vmware-classic.md) Azure'da çalışan başarısız üzerinden makinelerinizi şirket içi ortamınız için yeniden getirir.
