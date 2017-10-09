---
title: "aaaHow VMware çoğaltma tooAzure iş Azure Site kurtarma mu? | Microsoft Belgeleri"
description: "Bu makalede bileşenleri ve çoğaltma VMware Vm'lerini ve fiziksel sunucuları tooAzure hello Azure Site Recovery hizmeti ile şirket içi kullanılan mimarisi genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-architecture
ms.openlocfilehash: f0fb834f8b251640f97e4d0163b2b9e54de691e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-vmware-replication-tooazure-work-in-site-recovery"></a>VMware çoğaltma tooAzure Site Recovery nasıl çalışır?

Bu makalede hello bileşenleri ve işlemler çoğaltırken söz konusu şirket içi VMware sanal makineleri ve Windows/Linux fiziksel sunucuları, tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hizmet.

Fiziksel şirket içi sunucuları tooAzure çoğaltıldığında çoğaltma kullanır de aynı bileşenleri ve süreçleri Bu farklılıklar ile VMware VM çoğaltma olarak hello:

- VMware VM yerine hello yapılandırma sunucusu için bir fiziksel sunucuda kullanabilirsiniz.
- Yeniden çalışma için bir yerinde VMware altyapısı gerekir. Geri tooa fiziksel makine kapatamazsınız.

Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Mimari bileşenler

Bir dizi bileşen dahil olan VMware Vm'lerini ve fiziksel sunucuları tooAzure çoğaltırken.

**Bileşen** | **Konum** | **Ayrıntılar**
--- | --- | ---
**Azure** | Azure’da bir Azure hesabına, bir Azure depolama hesabına ve bir Azure ağına ihtiyacınız vardır. | Çoğaltılan veriler hello depolama hesabında depolanır ve şirket içi sitenizdeki yük devretme durumunda Azure Vm'leri çoğaltılan hello verilerle oluşturulur. Hello Azure VM'ler, oluşturuldukları zaman toohello Azure sanal ağı bağlayın.
**Yapılandırma sunucusu** | Tek bir yönetim sunucusu (VMWare VM) hello yapılandırma sunucusuna işlem sunucusu, ana hedef sunucusu da dahil olmak üzere hello dağıtım için gerekli tüm hello şirket içi bileşenleri çalıştıran şirket içi | Merhaba yapılandırma sunucusu bileşeni şirket içi ve Azure arasındaki iletişimi düzenler ve veri çoğaltma işlemlerini yönetir.
 **İşlem sunucusu**:  | Varsayılan olarak hello yapılandırma sunucusunda yüklü. | Çoğaltma ağ geçidi olarak davranır. Çoğaltma verilerini alıp, önbelleğe alma, sıkıştırma ve şifreleme iyileştirir ve tooAzure depolama gönderir.<br/><br/> Merhaba işlem sunucusu da hello Mobility hizmeti tooprotected makinelere göndermeli yüklemesini işler ve VMware vm'lerinin otomatik bulma işlemini gerçekleştirir.<br/><br/> Dağıtımınız büyüdükçe, çoğaltma trafik artırma ek ayrı adanmış işlem sunucuları toohandle ekleyebilirsiniz.
 **Ana hedef sunucu** | Merhaba şirket içi yapılandırma sunucusu üzerinde varsayılan olarak yüklüdür. | Azure’dan yeniden çalışma sırasında çoğaltma verilerini işler.<br/><br/> Yeniden çalışma trafiğinin hacmi yüksekse, yeniden çalışma için ayrı bir ana hedef sunucu dağıtabilirsiniz.
**VMware sunucuları** | VMware Vm'lerini vSphere ESXi sunucularda barındırılan ve bir vCenter server toomanage hello konakları öneririz. | VMware sunucularını tooyour kurtarma Hizmetleri kasası ekleyin.
**Çoğaltılan makineler** | Merhaba Mobility hizmeti her VMware tooreplicate istediğiniz VM yüklenir. El ile her makinede veya hello işlem sunucusu anında yüklemesinden ile yüklenebilir.

Merhaba dağıtımının önkoşulları ve hello de bu bileşenlerin her birini gereksinimleri hakkında bilgi edinin [destek matrisi](site-recovery-support-matrix-to-azure.md).

**Şekil 1: VMware tooAzure bileşenleri**

![Bileşenler](./media/site-recovery-components/arch-enhanced.png)

## <a name="replication-process"></a>Çoğaltma işlemi

1. Azure bileşenleri ve bir kurtarma Hizmetleri kasası gibi hello dağıtım, ayarlayın. Merhaba kasasına hello çoğaltma kaynak ve hedef hello yapılandırma sunucusunu ayarlamayı, VMware sunucularını ekleyin, bir çoğaltma ilkesi oluşturun, hello Mobility hizmeti dağıtmak, çoğaltmayı etkinleştirmek ve yük devretme testi çalıştırmak belirtin.
2.  Merhaba çoğaltma ilkesiyle uygun şekilde çoğaltma makineleri başlatmayın ve bir başlangıç hello verilerin çoğaltılmış tooAzure depolama kopyasıdır.
4. Merhaba ilk çoğaltma sonlandırıldıktan sonra delta değişiklikleri tooAzure çoğaltma başlar. Bir makine için izlenen değişiklikler bir .hrl dosyasında saklanır.
    - Çoğaltma HTTPS 443 numaralı bağlantı noktasında hello yapılandırma sunucusuyla gelen çoğaltma yönetimi için iletişim kurar.
    - Çoğaltılan makineler Gönder çoğaltma verileri toohello işlem sunucusu HTTPS 9443 bağlantı noktasına gelen (yapılandırılabilir).
    - Merhaba yapılandırma sunucusu Azure ile çoğaltma yönetimi HTTPS 443 giden bağlantı noktası üzerinden düzenler.
    - Merhaba işlem sunucusu kaynak makinelerden verileri alan, en iyi duruma getirir ve bunu şifreler ve tooAzure depolama bağlantı noktası 443 üzerinden giden gönderir.
    - Çoklu VM tutarlılığını etkinleştirmek, ardından hello çoğaltma grubundaki birbiriyle 20004 bağlantı noktası üzerinden iletişim kurar. Çoklu VM, birden çok makineyi yük devrettikleri zaman kilitlenmeyle tutarlı ve uygulamayla tutarlı kurtarma noktalarını paylaşan çoğaltma grupları halinde gruplandırdığınızda kullanılır. Bu makineler çalışıyorsa yararlıdır hello aynı iş yükünü ve toobe tutarlı gerekir.
5. Trafiğidir çoğaltılmış tooAzure depolama ortak uç noktaları, üzerinde Internet hello. Alternatif olarak, Azure ExpressRoute [genel eşliğini](../expressroute/expressroute-circuit-peerings.md#public-peering) kullanabilirsiniz. Bir siteden siteye VPN bağlantısını bir şirket içi site tooAzure üzerinden trafik çoğaltma desteklenmiyor.

**Şekil 2: VMware tooAzure çoğaltma**

![Gelişmiş](./media/site-recovery-components/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Yük devretme ve yeniden çalışma işlemi

1. Yük devretme sınaması beklenen şekilde çalıştığını doğruladıktan sonra planlanmamış yük devretmeler tooAzure gerektiği gibi çalıştırabilirsiniz. Planlanan yük devretme desteklenmez.
2. Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md), birden çok VM üzerinden toofail.
3. Yük devretme işlemini çalıştırdığınızda Azure’da çoğaltma sanal makineleri oluşturulur. Bir yük devretme toostart erişilirken hello iş yükü Azure VM hello çoğaltmasından uygulayın.
4. Birincil şirket içi siteniz yeniden kullanılabilir olduğunda siteyi yeniden çalıştırabilirsiniz. Bir yeniden çalışma altyapısını ayarlamak, hello makine hello ikincil site toohello birincil çoğaltma işlemi başlatma ve hello ikincil siteden planlanmamış bir yük devretme çalıştırın. Bu yük devretme yürüttükten sonra veri arka şirket içi olur ve yeniden tooenable çoğaltma tooAzure gerekir. [Daha fazla bilgi](site-recovery-failback-azure-to-vmware.md)

Birkaç yeniden çalışma gereksinimi vardır:


- **Azure'da geçici işlem sunucusu**: toofail geri azure'dan yük devretme sonrasında istiyorsanız Azure toohandle çoğaltmadan bir işlem sunucusu olarak yapılandırılan bir Azure VM yukarı tooset gerekir. Yeniden çalışma sona erdikten sonra bu VM'yi silebilirsiniz.
- **VPN bağlantısı**: hello Azure ağ toohello şirket içi siteden gerekir yeniden çalışma için bir VPN bağlantısı (veya Azure ExpressRoute) ayarlayın.
- **Ayrı şirket içi ana hedef sunucusu**: hello şirket içi ana hedef sunucusu yeniden çalışma işlemini yürütür. Hello ana hedef sunucusu varsayılan olarak hello yönetim sunucusunda yüklü, ancak daha fazla hacimli trafikte çalıştırma işlemini gerçekleştiriyorsanız bu amaç için bir ayrı şirket içi ana hedef sunucusu ayarlamanız gerekir.
- **Yeniden çalışma ilkesi**: tooreplicate geri tooyour şirket içi site, bir yeniden çalışma ilkesi gerekir. Bu ilke çoğaltma ilkenizi oluşturduğunuzda otomatik olarak oluşturulur.
- **VMware altyapı**: geri başarısız olması tooan şirket içi VMware VM. Şirket içi fiziksel sunucuların tooAzure çoğaltıyorsanız bile bu, bir şirket içi VMware altyapı ihtiyacınız anlamına gelir.

**Şekil 3: VMware/fiziksel yeniden çalışma**

![Yeniden çalışma](./media/site-recovery-components/enhanced-failback.png)


## <a name="next-steps"></a>Sonraki adımlar

Gözden geçirme hello [destek matrisi](site-recovery-support-matrix-to-azure.md)
