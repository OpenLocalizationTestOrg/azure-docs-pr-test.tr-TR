---
title: "Site Recovery iş aaaHow mu? | Microsoft Belgeleri"
description: "Bu makalede Site Recovery mimarisine genel bir bakış sağlanır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Azure Site Recovery, şirket içi altyapılarında nasıl kullanılır?

> [!div class="op_single_selector"]
> * [Azure sanal makinelerini çoğaltma](site-recovery-azure-to-azure-architecture.md)
> * [Şirket içi makineleri çoğaltma](site-recovery-components.md)

Bu makalede temel mimarisini hello [Azure Site Recovery](site-recovery-overview.md) hizmeti ve onu hello bileşenleri çalışma şirket içi tooAzure iş yükleri çoğaltmak için.

Bu makalenin veya hello hello altındaki tüm yorumlar sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-tooazure"></a>TooAzure Çoğalt

Çoğaltma ve şirket içi altyapı tooAzure hello şu koruyun:

- **VMware**: [Desteklenen bir ana bilgisayarda](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers) çalışan yerinde VMware sanal makineleri. [Desteklenen işletim sistemlerini](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) çalıştıran VMware sanal makinelerini çoğaltabilirsiniz
- **Hyper-V**: [Desteklenen bir ana bilgisayarda](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers) çalışan yerinde Hyper-V sanal makineleri.
- **Fiziksel makineler**: [Desteklenen işletim sistemlerinde](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) Windows veya Linux çalıştıran yerinde fiziksel sunucular. [Hyper-V ve Azure tarafından desteklenen](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) herhangi bir konuk işletim sistemini çalıştıran Hyper-V VM’lerini çoğaltabilirsiniz.

## <a name="vmware-tooazure"></a>VMware tooAzure

İşte VMware Vm'lerini tooAzure çoğaltmak için gerekir.

Alan | Bileşen | Ayrıntılar
--- | --- | ---
**Yapılandırma sunucusu** | Tek bir yönetim sunucusu (VMWare VM), tüm yerinde bileşenlerde (yapılandırma sunucusu, işlem sunucusu, ana hedef sunucusu) çalışır | Hello yapılandırma sunucusu şirket içi ve Azure arasındaki iletişimi düzenler ve veri çoğaltma işlemlerini yönetir.
 **İşlem sunucusu**:  | Varsayılan olarak hello yapılandırma sunucusunda yüklü. | Çoğaltma ağ geçidi olarak davranır. Çoğaltma verilerini alıp, önbelleğe alma, sıkıştırma ve şifreleme iyileştirir ve tooAzure depolama gönderir.<br/><br/> Merhaba işlem sunucusu da hello Mobility hizmeti tooprotected makinelere göndermeli yüklemesini işler ve VMware vm'lerinin otomatik bulma işlemini gerçekleştirir.<br/><br/> Dağıtımınız büyüdükçe, çoğaltma trafik artırma ek ayrı adanmış işlem sunucuları toohandle ekleyebilirsiniz.
 **Ana hedef sunucu** | Merhaba şirket içi yapılandırma sunucusu üzerinde varsayılan olarak yüklüdür. | Azure’dan yeniden çalışma sırasında çoğaltma verilerini işler.<br/><br/> Yeniden çalışma trafiğinin hacmi yüksekse, yeniden çalışma için ayrı bir ana hedef sunucu dağıtabilirsiniz.
**VMware sunucuları** | VMware Vm'lerini vSphere ESXi sunucularda barındırılan ve bir vCenter server toomanage hello konakları öneririz. | VMware sunucularını tooyour kurtarma Hizmetleri kasası ekleyin.<br/><br/>
**Çoğaltılan makineler** | Merhaba Mobility hizmeti her VMware tooreplicate istediğiniz VM yüklenir. El ile her makinede veya hello işlem sunucusu anında yüklemesinden ile yüklenebilir.| -

**Şekil 1: VMware tooAzure bileşenleri**

![Bileşenler](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Çoğaltma işlemi

1. Azure bileşenleri ve bir kurtarma Hizmetleri kasası gibi hello dağıtım, ayarlayın. Merhaba kasasına hello çoğaltma kaynak ve hedef hello yapılandırma sunucusunu ayarlamayı, VMware sunucularını ekleyin, bir çoğaltma ilkesi oluşturun, hello Mobility hizmeti dağıtmak, çoğaltmayı etkinleştirmek ve yük devretme testi çalıştırmak belirtin.
2.  Merhaba çoğaltma ilkesiyle uygun şekilde çoğaltma makineleri başlatmayın ve bir başlangıç hello verilerin çoğaltılmış tooAzure depolama kopyasıdır.
4. Merhaba ilk çoğaltma sonlandırıldıktan sonra delta değişiklikleri tooAzure çoğaltma başlar. Bir makine için izlenen değişiklikler bir .hrl dosyasında saklanır.
    - Çoğaltma HTTPS 443 numaralı bağlantı noktasında hello yapılandırma sunucusuyla gelen çoğaltma yönetimi için iletişim kurar.
    - Çoğaltılan makineler Gönder çoğaltma verileri toohello işlem sunucusu HTTPS 9443 bağlantı noktasına gelen (yapılandırılabilir).
    - Merhaba yapılandırma sunucusu Azure ile çoğaltma yönetimi HTTPS 443 giden bağlantı noktası üzerinden düzenler.
    - Merhaba işlem sunucusu kaynak makinelerden verileri alan, en iyi duruma getirir ve bunu şifreler ve tooAzure depolama bağlantı noktası 443 üzerinden giden gönderir.
    - Çoklu VM tutarlılığını etkinleştirmek, ardından hello çoğaltma grubundaki birbiriyle 20004 bağlantı noktası üzerinden iletişim kurar. Çoklu VM, birden çok makineyi yük devrettikleri zaman kilitlenmeyle tutarlı ve uygulamayla tutarlı kurtarma noktalarını paylaşan çoğaltma grupları halinde gruplandırdığınızda kullanılır. Bu makineler çalışıyorsa yararlıdır hello aynı iş yükünü ve toobe tutarlı gerekir.
5. Trafiğidir çoğaltılmış tooAzure depolama ortak uç noktaları, üzerinde Internet hello. Alternatif olarak, Azure ExpressRoute [genel eşliğini](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering) kullanabilirsiniz. Bir siteden siteye VPN bağlantısını bir şirket içi site tooAzure üzerinden trafik çoğaltma desteklenmiyor.

**Şekil 2: VMware tooAzure çoğaltma**

![Gelişmiş](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Yük devretme ve yeniden çalışma

1. Yük devretme sınaması beklenen şekilde çalıştığını doğruladıktan sonra planlanmamış yük devretmeler tooAzure gerektiği gibi çalıştırabilirsiniz. Planlanan yük devretme desteklenmez.
2. Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md), birden çok VM üzerinden toofail.
3. Yük devretme işlemini çalıştırdığınızda Azure’da çoğaltma sanal makineleri oluşturulur. Bir yük devretme toostart erişilirken hello iş yükü Azure VM hello çoğaltmasından uygulayın.
4. Birincil şirket içi siteniz yeniden kullanılabilir olduğunda siteyi yeniden çalıştırabilirsiniz. Bir yeniden çalışma altyapısını ayarlamak, hello makine hello ikincil site toohello birincil çoğaltma işlemi başlatma ve hello ikincil siteden planlanmamış bir yük devretme çalıştırın. Bu yük devretme yürüttükten sonra veri arka şirket içi olur ve yeniden tooenable çoğaltma tooAzure gerekir. [Daha fazla bilgi](site-recovery-failback-azure-to-vmware.md)

**Şekil 3: VMware/fiziksel yeniden çalışma**

![Yeniden çalışma](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>Fiziksel tooAzure

Fiziksel şirket içi sunucuları tooAzure çoğaltıldığında çoğaltma kullanır de aynı bileşenleri ve süreçleri olarak hello [VMware tooAzure](#vmware-replication-to-azure), ancak bu farklılıklar dikkat edin:

- VMware VM yerine hello yapılandırma sunucusu için bir fiziksel sunucuda kullanabilirsiniz
- Yeniden çalışma için bir yerinde VMware altyapısı gerekir. Geri tooa fiziksel makine kapatamazsınız.

## <a name="hyper-v-tooazure"></a>Hyper-V tooAzure

### <a name="replication-process"></a>Çoğaltma işlemi

1. Hello Azure bileşenleri ayarlayın. Site Recovery dağıtımına başlamadan önce depolama ve ağ hesapları ayarlamanızı öneririz.
2. Site Recovery kurtarma için bir Kurtarma Hizmetleri kasası ayarlarsınız ve aşağıdakileri de içeren kasa ayarlarını yapılandırırsınız:
    - Kaynak ve hedef ayarları. Hyper-V konakları VMM bulutunda değil yönetiyorsanız, hello hedefi için bir Hyper-V sitesi kapsayıcı oluşturun ve Hyper-V konakları tooit ekleyin. Hyper-V konakları VMM yönetiliyorsa hello hello VMM bulut kaynağıdır. Merhaba, Azure hedefidir.
    - Hello Azure Site Recovery sağlayıcısı ve hello Microsoft Azure kurtarma Hizmetleri Aracısı yüklemesi. Sağlayıcı üzerinde yüklü ve her Hyper-V ana bilgisayarda aracı hello VMM hello varsa. VMM yoksa, hello sağlayıcı ve aracı her ana bilgisayarda yüklü.
    - Merhaba Hyper-V sitesi ya da VMM bulutu için bir çoğaltma ilkesi oluşturun. Merhaba, uygulanan tooall VM'ler hello site veya Bulut ana bilgisayar üzerindeki ilkesidir.
    - Hyper-V VM’leri için çoğaltmayı etkinleştirirsiniz. İlk çoğaltma hello Çoğaltma İlkesi ayarlarına uygun şekilde gerçekleştirilir.
4. Veri değişiklikleri izlenir ve delta değişiklikleri tooAzure çoğaltmasını hello ilk çoğaltma sonlandırıldıktan sonra başlar. Bir öğe için izlenen değişiklikler bir .hrl dosyasında saklanır.
5. Bir test yük devretme toomake emin çalıştırmadan her şeyi çalışmaktadır.

### <a name="failover-and-failback-process"></a>Yük devretme ve yeniden çalışma işlemi

1. Planlanmış çalıştırabilirsiniz veya planlanmamış [yük devretme](site-recovery-failover.md) şirket içi Hyper-V sanal makineleri tooAzure gelen. Planlanmış bir yük devretme çalıştırın, sonra kaynak VM'ler tooensure kapatın, veri kaybı.
2. Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md) birden fazla makine tooorchestrate yük devretme.
4. Merhaba yük devretme çalıştırdıktan sonra çoğaltma sanal makineleri Azure üzerinde oluşturulan mümkün toosee hello olmalıdır. Gerekli olursa, ortak bir IP adresi toohello VM atayabilirsiniz.
5. Ardından Azure VM hello çoğaltmasından hello iş yükü erişme hello yük devretme toostart yürüttükten.
6. Birincil yerinde siteniz yeniden kullanılabilir olduğunda siteyi [yeniden çalıştırabilirsiniz](site-recovery-failback-from-azure-to-hyper-v.md). Planlanmış bir yük devretme Azure toohello birincil siteden kapalı tetiklersiniz. Yapabilecekleriniz planlanmış bir yük devretme için aynı VM veya tooan alternatif konumu ve eşitleme select toofailback toohello veri kaybı Azure ve şirket içi, tooensure arasında değişir. Şirket içi sanal makineleri oluştururken hello yük devretme uygulayın.

**Şekil 4: Hyper-V sitesi tooAzure çoğaltma**

![Bileşenler](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Şekil 5: Hyper-V, VMM Bulutları tooAzure çoğaltma**

![Bileşenler](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>Tooa ikincil siteye çoğaltma

İkincil site tooyour aşağıdaki hello çoğaltabilirsiniz:

- **VMware**: [Desteklenen bir ana bilgisayarda](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) çalışan yerinde VMware sanal makineleri. [Desteklenen işletim sistemlerini](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions) çalıştıran VMware sanal makinelerini çoğaltabilirsiniz
- **Fiziksel makineler**: [Desteklenen işletim sistemlerinde](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions) Windows veya Linux çalıştıran yerinde fiziksel sunucular.
- **Hyper-V**: VMM bulutlarında yönetilen [desteklenen Hyper-V ana bilgisayarlarında](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) çalışan yerinde Hyper-V sanal makineleri. [desteklenen ana bilgisayarlar](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). [Hyper-V ve Azure tarafından desteklenen](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) herhangi bir konuk işletim sistemini çalıştıran Hyper-V VM’lerini çoğaltabilirsiniz.


## <a name="vmwarephysical-tooa-secondary-site"></a>VMware/fiziksel tooa ikincil site

VMware Vm'lerini veya fiziksel sunucuları tooa ikincil site Inmage Scout kullanarak çoğaltılır.

### <a name="components"></a>Bileşenler

**Alan** | **Bileşen** | **Ayrıntılar**
--- | --- | ---
**İşlem sunucusu** | Birincil sitede bulunur | Merhaba işlem sunucusu toohandle önbelleğe alma, sıkıştırma ve veri iyileştirme dağıtın.<br/><br/> Ayrıca, göndermeli yüklemesi hello tooprotect istediğiniz birleşik aracı toomachines yürütür.
**Yapılandırma sunucusu** | İkincil sitede bulunur | Hello yapılandırma sunucusu yönetir, yapılandırma ve dağıtımınız, ya da izleme hello Yönetim Web sitesini veya hello vContinuum konsolunu kullanarak.
**vContinuum sunucusu** | İsteğe bağlı. Hello aynı yüklü konumu hello yapılandırma sunucusu olarak. | Korunan ortamınızı yönetmeye ve izlemeye yönelik bir konsol sağlar.
**Ana hedef sunucu** | Merhaba ikincil sitede bulunan | Merhaba ana hedef sunucusu çoğaltılan verileri tutar. Merhaba işlem sunucusundan verileri alır, hello ikincil sitede çoğaltılan bir makine oluşturur ve hello veri bekletme noktalarını tutar.<br/><br/> Merhaba ihtiyacınız olan ana hedef sunucusu sayısı koruduğunuz makine hello sayısına bağlıdır.<br/><br/> Toofail geri toohello birincil site istiyorsanız, bir ana hedef sunucusu var. çok gerekir. Merhaba birleşik aracı bu sunucuda yüklü.
**VMware ESX/ESXi ve vCenter sunucusu** |  VM’ler ESX/ESXi ana bilgisayarlarında barındırılır. Ana bilgisayarlar bir vCenter sunucusu ile yönetilir | Bir VMware altyapı tooreplicate VMware Vm'lerini gerekir.
**VM’ler/fiziksel sunucular** |  VMware Vm'lerini ve fiziksel sunucularda tooreplicate istediğiniz yüklenen birleşik aracı. | Merhaba aracı hello bileşenlerinin tümünü arasındaki bir iletişim sağlayıcısı gibi davranır.


### <a name="replication-process"></a>Çoğaltma işlemi

1. Merhaba bileşen sunucularını (yapılandırma, işlem, ana hedef) her sitede ayarlayın ve tooreplicate istediğiniz makinelere hello birleşik aracı yükleyin.
2. İlk çoğaltma sonrasında hello aracı her makinede delta çoğaltma değişiklikleri toohello işlem sunucusuna gönderir.
3. Merhaba işlem sunucusu hello verileri iyileştirir ve hello ikincil sitede toohello ana hedef sunucusuna aktarır. Merhaba yapılandırma sunucusu hello çoğaltma sürecini yönetir.

**Şekil 6: VMware tooVMware çoğaltma**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Hyper-V tooa ikincil site

İşte Hyper-V sanal makineleri tooa ikincil site çoğaltmak için gerekir.


**Alan** | **Bileşen** | **Ayrıntılar**
--- | --- | ---
**VMM sunucusu** | Bir VMM sunucusunun hello birincil sitede ve hello ikincil sitedeki öneririz | Her bir VMM sunucusunun bağlı toohello olmalıdır Internet.<br/><br/> Her sunucu en az bir VMM özel bulut, Hyper-V hello yetenek profili kümesine sahip olması gerekir.<br/><br/> Hello Azure Site Recovery sağlayıcısı hello VMM sunucusuna yükleyin. Merhaba sağlayıcı düzenler ve çoğaltma hello Site Recovery hizmeti ile Merhaba yönetir Internet. Merhaba sağlayıcı ile Azure arasındaki iletişimler güvenli ve şifrelidir.
**Hyper-V sunucusu** |  Bir veya daha fazla Hyper-V ana bilgisayar sunucuları hello birincil ve ikincil VMM bulutlarında.<br/><br/> Sunucuları bağlı toohello olmalıdır Internet.<br/><br/> Veri hello LAN veya Kerberos veya sertifika kimlik doğrulaması kullanarak VPN üzerinden hello birincil ve ikincil Hyper-V ana bilgisayar sunucuları arasında çoğaltılır.  
**Hyper-V VM’leri** | Merhaba kaynak Hyper-V konak sunucusunda bulunan. | Merhaba kaynak ana bilgisayar sunucusunun tooreplicate istediğiniz en az bir VM'ye sahip olması gerekir.

### <a name="replication-process"></a>Çoğaltma işlemi

1. Azure hesabı hello ayarlayın.
2. Site Recovery kurtarma için bir Kurtarma Hizmetleri kasası ayarlarsınız ve aşağıdakileri de içeren kasa ayarlarını yapılandırırsınız:

    - Merhaba çoğaltma kaynağı ve hedefi (birincil ve ikincil siteler).
    - Hello Azure Site Recovery sağlayıcısı ve hello Microsoft Azure kurtarma Hizmetleri Aracısı yüklemesi. Merhaba sağlayıcı VMM sunucuları ve hello Aracısı her Hyper-V ana bilgisayarda yüklü.
    - Kaynak VMM bulutu için bir çoğaltma ilkesi oluşturursunuz. Merhaba, uygulanan tooall hello bulut ana bilgisayarda yer alan VM'ler ilkesidir.
    - Hyper-V VM’leri için çoğaltmayı etkinleştirirsiniz. İlk çoğaltma hello Çoğaltma İlkesi ayarlarına uygun şekilde gerçekleştirilir.
4. Veri değişiklikleri izlenir ve hello ilk çoğaltma sonlandırıldıktan sonra değişim çoğaltması toobegins değiştirir. Bir öğe için izlenen değişiklikler bir .hrl dosyasında saklanır.
5. Bir test yük devretme toomake emin çalıştırmadan her şeyi çalışmaktadır.

**Şekil 7: VMM tooVMM çoğaltma**

![Şirket içi tooon içi](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Yük devretme ve yeniden çalışma

1. Şirket içi siteler arasında planlanmış veya planlanmamış bir [yük devretme](site-recovery-failover.md) gerçekleştirebilirsiniz. Planlanmış bir yük devretme çalıştırın, sonra kaynak VM'ler tooensure kapatın, veri kaybı.
2. Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md) birden fazla makine tooorchestrate yük devretme.
4. Merhaba yük devretme makineler hello ikincil konumdaki sonra bir planlanmamış yük devretme tooa ikincil site gerçekleştirirseniz koruma veya çoğaltma için etkin değil. Planlanmış bir yük devretme hello yük devretme sonrasında çalıştırdıysanız hello ikincil konumdaki makineler korunur.
5. Ardından, VM hello çoğaltmasından hello yük devretme toostart erişilirken hello iş yükü uygulayın.
6. Birincil sitenizi yeniden kullanılabilir duruma geldiğinde, çoğaltmayı tersine çevirme tooreplicate hello ikincil site toohello birincil gelen başlatır. Çoğaltmayı tersine çevirme hello sanal makineleri korumalı bir duruma getirir, ancak hello ikincil veri merkezine hala hello etkin konumdur.
7. toomake hello birincil site hello etkin konuma yeniden planlı bir yük devretme ikincil tooprimary, başka bir tersine çoğaltma tarafından izlenen işlemini başlatır.


## <a name="next-steps"></a>Sonraki adımlar

- [Daha fazla bilgi edinin](site-recovery-hyper-v-azure-architecture.md) hello Hyper-V çoğaltma iş akışı hakkında.
- [Önkoşulları denetleme](site-recovery-prereq.md)
