---
title: "Fiziksel sunucu çoğaltma için Azure Site Kurtarma'yı kullanarak Azure Mimarisi gözden | Microsoft Docs"
description: "Bu makalede, bileşenleri ve Azure Site Recovery hizmeti ile şirket içi fiziksel sunucuların Azure'a çoğaltırken kullanılan mimariye genel bakış sağlar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 09c9b136-35f5-465e-8d0f-f4c5d5d9f880
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 843c3f1b54f50fe50b162ed242deab717a080830
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-1-review-the-architecture-for-physical-server-replication-to-azure"></a>1. adım: Gözden geçirme fiziksel sunucu çoğaltma Azure için mimarisi

Bu makalede bileşenleri ve şirket içi Windows/Linux fiziksel sunucuları Azure'a çoğaltırken kullanılan işlemleri kullanarak [Azure Site Recovery](site-recovery-overview.md) hizmet.

Tüm yorumlarınızı bu makalenin alt kısmında paylaşabilir veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda soru sorabilirsiniz.


## <a name="architectural-components"></a>Mimari bileşenler

Tablo gereksinim duyduğunuz bileşenleri özetler.

**Bileşen** | **Gereksinim** | **Ayrıntılar**
--- | --- | ---
**Azure** | Bir Azure hesabı, bir Azure depolama hesabı ve bir Azure ağı gerekir. | Çoğaltılan veriler depolama hesabında depolanır ve yük devretme durumunda Azure Vm'leri çoğaltılan veriler ile oluşturulur. Bunlar oluşturulduğunda azure sanal makineleri Azure sanal ağına bağlayın.
**Yapılandırma sunucusu** | Tek bir tüm şirket içi Site Recovery bileşenlerini çalıştıran yönetim sunucusu (fiziksel sunucu veya VMware VM) şirket içi. Bunlar bir yapılandırma sunucusuna işlem sunucusu, ana hedef sunucusu içerir. | Yapılandırma sunucusu bileşeni, şirket içi ile Azure arasındaki iletişimi düzenler ve veri çoğaltma işlemlerini yönetir.
 **İşlem sunucusu**  | Varsayılan olarak yapılandırma sunucusuna yüklenir. | Çoğaltma ağ geçidi olarak davranır. Çoğaltma verilerini alıp bu verileri önbelleğe alma, sıkıştırma ve şifreleme işlemleriyle iyileştirir ve Azure depolama alanına gönderir.<br/><br/> İşlem sunucusu ayrıca Mobility hizmetinin korunan makinelere göndermeli yüklemesini işler.<br/><br/> Artan hacimli çoğaltma trafiğini işlemek için ek ayrı adanmış işlem sunucuları ekleyebilirsiniz.
 **Ana hedef sunucu** | Varsayılan olarak şirket içi yapılandırma sunucusuna yüklenir. | Azure’dan yeniden çalışma sırasında çoğaltma verilerini işler.<br/><br/> Yeniden çalışma trafiğinin hacmi yüksekse, yeniden çalışma için ayrı bir ana hedef sunucu dağıtabilirsiniz.
**Çoğaltılmış sunucuları** | Mobility hizmeti bileşeninin çoğaltmak istediğiniz her Windows/Linux sunucusuna yüklenir. Her makineye el ile yüklenebileceği gibi, işlem sunucusundan göndererek yükleme yoluyla da yüklenebilir.
**İlk duruma döndürme** | Yeniden çalışma için bir VMware altyapı gereklidir. Bir fiziksel sunucuda yeniden çalışamazsınız.


**Şekil 1: Fiziksel Azure bileşenleri**

![Bileşenler](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Çoğaltma işlemi

1. Şirket içi ve Azure bileşenleri de dahil olmak üzere dağıtım, ayarlayın. Kurtarma Hizmetleri kasasına çoğaltma kaynak ve hedef yapılandırma sunucusunu ayarlamayı, bir çoğaltma ilkesi oluşturun Mobility hizmeti dağıtmak, çoğaltmayı etkinleştirmek ve yük devretme testi çalıştırmak belirtin.
2.  Makinelerin çoğaltılacağı Çoğaltma İlkesi ve bir başlangıç kopyasını veri uygun olarak Azure depolama alanına çoğaltılır.
4. İlk çoğaltma sonlandırıldıktan sonra Azure delta değişikliklerini başlar. Bir makine için izlenen değişiklikler bir .hrl dosyasında saklanır.
    - Çoğaltılan makineler çoğaltma yönetimi için HTTPS 443 gelen bağlantı noktasındaki yapılandırma sunucusuyla iletişim kurar.
    - Çoğaltılan makinelerin çoğaltma veri gönderme bağlantı noktası HTTPS 9443 işlem sunucusu için gelen (değiştirilmiş).
    - Yapılandırma sunucusu, HTTPS 443 giden bağlantı noktası üzerinden Azure ile çoğaltma yönetimini düzenler.
    - İşlem sunucusu kaynak makinelerden gelen verileri alır, iyileştirip şifreler ve 443 giden bağlantı noktası üzerinden Azure depolamaya gönderir.
    - Çoklu VM tutarlılığını etkinleştirirseniz çoğaltma grubundaki makineler birbiriyle 20004 bağlantı noktası üzerinden iletişim kurar. Çoklu VM, birden çok makineyi yük devrettikleri zaman kilitlenmeyle tutarlı ve uygulamayla tutarlı kurtarma noktalarını paylaşan çoğaltma grupları halinde gruplandırdığınızda kullanılır. Bu özellik, makinelerin aynı iş yükünü çalıştırdığı ve tutarlı olmasının gerektiği durumlarda kullanışlıdır.
5. Trafik İnternet üzerinden Azure depolama genel uç noktalarına çoğaltılır. Alternatif olarak, Azure ExpressRoute [genel eşliğini](../expressroute/expressroute-circuit-peerings.md#public-peering) kullanabilirsiniz. Trafiğin siteden siteye bir VPN aracılığıyla şirket içi bir siteden Azure’a çoğaltılması desteklenmez.

**Şekil 2: Fiziksel Azure çoğaltma**

![Gelişmiş](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Yük devretme ve yeniden çalışma işlemi

Yük devretme testinin beklenen şekilde çalıştığını doğruladıktan sonra, gerektiğinde Azure’a planlanmamış yük devretmeler çalıştırabilirsiniz. Bir yük devretme çalıştırdığınızda, Azure Vm'leri çoğaltılmış verilerden oluşturulur. Birincil şirket içi sitenize yeniden kullanılabilir duruma geldiğinde, daha sonra geri yük devredebilir. Şunlara dikkat edin:

- Planlanan yük devretme desteklenmez.
- Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md), birden çok makinede yük birlikte başarısız.
- Kopya Azure VM’sindeki iş yüküne erişmeye başlamak için bir yük devretme yürütürsünüz.
- Birincil sitenin yeniden kullanılabilir duruma geldiğinde, makine birincil siteye ikincil çoğaltma. Ardından, ikincil siteden planlanmamış bir yük devretme çalıştırın. Bu yük devretme yürütüldükten sonra, veriler şirket içine döner ve Azure’a çoğaltmayı yeniden etkinleştirmeniz gerekir.

Yeniden çalışma bileşenleri şunları içerir:

- **Azure'da geçici işlem sunucusu**: Azure VM'yi yedekleme azure'dan çoğaltmayı düzenlemek için bir işlem sunucusu olarak davranacak şekilde ayarlamanız gerekir. Yeniden çalışma sona erdikten sonra bu VM'yi silebilirsiniz.
- **VPN bağlantısı**:, bir VPN bağlantısı (veya Azure ExpressRoute) Azure ağından şirket içi siteye gerekir.
- **Ayrı şirket içi ana hedef sunucusu**: (varsayılan olarak yapılandırma sunucusunda yüklü) şirket içi ana hedef sunucusu yeniden çalışma işlemini yürütür. Geri büyük miktarda trafik başarısız olursa, bu amaçla bir ayrı şirket içi ana hedef sunucusu ayarlamanız gerekir.
- **Yeniden çalışma ilkesi**: geri dönme ilkesini gerekir. Bu ilke çoğaltma ilkenizi oluşturduğunuzda otomatik olarak oluşturulur.
- **VMware altyapısı**: Bir şirket içi VMware VM'ye geri dönmeniz gerekir. Bu, şirket içi fiziksel sunucuları Azure'a çoğaltıyor olsanız bile şirket içi VMware altyapısına ihtiyacınız olduğu anlamına gelir.

**Şekil 3: Fiziksel sunucuya geri dönme**

![Yeniden çalışma](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Sonraki adımlar

Git [2. adım: Önkoşullar ve sınırlamalar doğrulayın](physical-walkthrough-prerequisites.md)
