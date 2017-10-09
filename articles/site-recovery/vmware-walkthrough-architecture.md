---
title: "VMware çoğaltma tooAzure için aaaReview hello mimarisi | Microsoft Docs"
description: "Bu makalede, bileşenleri ve hello Azure Site Recovery hizmeti ile şirket içi VMware sanal makinelerini tooAzure çoğaltırken kullanılan mimariye genel bakış sağlar"
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
ms.topic: article
ms.date: 06/27.017
ms.author: raynew
ms.openlocfilehash: 7acb1d8e83a846dca79e175fd1af9324f2c31e65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-vmware-replication-tooazure"></a>1. adım: VMware çoğaltma tooAzure hello mimarisi gözden geçirin

Bu makalede hello bileşenleri ve süreçleri çoğaltma VMware sanal makineleri tooAzure hello kullanarak şirket içi kullanılan [Azure Site Recovery](site-recovery-overview.md) hizmet.

Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Mimari bileşenler

Merhaba tablo ihtiyacınız hello bileşenleri özetler.

**Bileşen** | **Gereksinim** | **Ayrıntılar**
--- | --- | ---
**Azure** | Bir Azure aboneliği, Azure storage hesabı ve bir Azure ağı gerekir. | Çoğaltılan veriler hello depolama hesabında depolanır. Şirket içi sitenizdeki yük devretme durumunda azure Vm'leri çoğaltılan hello verilerle oluşturulur. Hello Azure VM'ler, oluşturuldukları zaman toohello Azure sanal ağı bağlayın.
**Yapılandırma sunucusu** | Tek bir yönetim sunucusu (VMware VM) tüm hello şirket içi hello dağıtımı için Site Recovery bileşenlerini çalıştıran şirket içi. Bunlar bir yapılandırma sunucusuna işlem sunucusu, ana hedef sunucusu içerir. | Merhaba yapılandırma sunucusu bileşeni şirket içi ve Azure arasındaki iletişimi düzenler ve veri çoğaltma işlemlerini yönetir.
 **İşlem sunucusu**:  | Varsayılan olarak hello yapılandırma sunucusunda yüklü. | Çoğaltma ağ geçidi olarak davranır. Çoğaltma verilerini alıp, önbelleğe alma, sıkıştırma ve şifreleme iyileştirir ve tooAzure depolama gönderir.<br/><br/> Merhaba işlem sunucusu da hello Mobility hizmeti tooprotected makinelere göndermeli yüklemesini işler ve VMware vm'lerinin otomatik bulma işlemini gerçekleştirir.<br/><br/> Dağıtımınız büyüdükçe, çoğaltma trafik artırma ek ayrı adanmış işlem sunucuları toohandle ekleyebilirsiniz.
 **Ana hedef sunucu** | Merhaba şirket içi yapılandırma sunucusu üzerinde varsayılan olarak yüklüdür. | Azure’dan yeniden çalışma sırasında çoğaltma verilerini işler.<br/><br/> Yeniden çalışma trafiğinin hacmi yüksekse, yeniden çalışma için ayrı bir ana hedef sunucu dağıtabilirsiniz.
**VMware sunucuları** | VMware Vm'lerini vSphere ESXi sunucularda barındırılan ve bir vCenter server toomanage hello konakları öneririz. | VMware sunucularını tooyour kurtarma Hizmetleri kasası ekleyin.
**Çoğaltılan makineler** | Merhaba Mobility hizmeti Çoğalttığınız her VMware VM yüklenir. El ile her makinede veya hello işlem sunucusu anında yüklemesinden ile yüklenebilir.

**Şekil 1: VMware tooAzure bileşenleri**

![Bileşenler](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Çoğaltma işlemi

1. Şirket içi ve Azure bileşenleri de dahil olmak üzere hello dağıtım, ayarlayın. Merhaba kurtarma Hizmetleri kasasına hello çoğaltma kaynak ve hedef hello yapılandırma sunucusunu ayarlamayı, bir çoğaltma ilkesi oluşturmak hello Mobility hizmeti dağıtmak, çoğaltmayı etkinleştirmek ve yük devretme testi çalıştırmak belirtin.
2. Makinelerin çoğaltılacağı hello Çoğaltma İlkesi ve bir başlangıç kopyasını hello veri uygun olarak çoğaltılmış tooAzure Depolama ' dir.
3. İlk çoğaltma sonlandırıldıktan sonra delta değişiklikleri tooAzure çoğaltmasını başlar. Bir makine için izlenen değişiklikler bir .hrl dosyasında saklanır.
    - Çoğaltma HTTPS 443 numaralı bağlantı noktasında hello yapılandırma sunucusuyla gelen çoğaltma yönetimi için iletişim kurar.
    - Çoğaltılan makineler Gönder çoğaltma verileri toohello işlem sunucusu HTTPS 9443 bağlantı noktasına gelen (değiştirilmiş).
    - Merhaba yapılandırma sunucusu Azure ile çoğaltma yönetimi HTTPS 443 giden bağlantı noktası üzerinden düzenler.
    - Merhaba işlem sunucusu kaynak makinelerden verileri alan, en iyi duruma getirir ve bunu şifreler ve tooAzure depolama bağlantı noktası 443 üzerinden giden gönderir.
    - Çoklu VM tutarlılığını etkinleştirmek, ardından hello çoğaltma grubundaki birbiriyle 20004 bağlantı noktası üzerinden iletişim kurar. Çoklu VM, birden çok makineyi yük devrettikleri zaman kilitlenmeyle tutarlı ve uygulamayla tutarlı kurtarma noktalarını paylaşan çoğaltma grupları halinde gruplandırdığınızda kullanılır. Bu makineler çalışıyorsa yararlıdır hello aynı iş yükünü ve toobe tutarlı gerekir.
4. Trafiğidir çoğaltılmış tooAzure depolama ortak uç noktaları, üzerinde Internet hello. Alternatif olarak, Azure ExpressRoute [genel eşliğini](../expressroute/expressroute-circuit-peerings.md#public-peering) kullanabilirsiniz. Bir siteden siteye VPN bağlantısını bir şirket içi site tooAzure üzerinden trafik çoğaltma desteklenmiyor.


**Şekil 2: VMware tooAzure çoğaltma**

![Gelişmiş](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

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

![Yeniden çalışma](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](vmware-walkthrough-prerequisites.md)
