---
title: "Azure Site RECOVERY'yi kullanarak fiziksel sunucu çoğaltma tooAzure için aaaReview hello mimarisi | Microsoft Docs"
description: "Bu makalede, bileşenleri ve hello Azure Site Recovery hizmeti ile şirket içi fiziksel sunucuların tooAzure çoğaltırken kullanılan mimariye genel bakış sağlar"
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
ms.openlocfilehash: 4f334c181fa6f0821adf978ebe9dbd7d36a3c753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-physical-server-replication-tooazure"></a>1. adım: Fiziksel sunucu çoğaltma tooAzure gözden geçirme hello mimarisi

Bu makalede hello bileşenleri ve süreçleri hello kullanarak şirket içi Windows/Linux fiziksel sunucuları tooAzure çoğaltırken kullanılan [Azure Site Recovery](site-recovery-overview.md) hizmet.

Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Mimari bileşenler

Merhaba tablo ihtiyacınız hello bileşenleri özetler.

**Bileşen** | **Gereksinim** | **Ayrıntılar**
--- | --- | ---
**Azure** | Bir Azure hesabı, bir Azure depolama hesabı ve bir Azure ağı gerekir. | Çoğaltılan veriler hello depolama hesabında depolanır ve yük devretme durumunda Azure Vm'leri çoğaltılan hello verilerle oluşturulur. Bunlar oluşturulduğunda azure VM'ler toohello Azure sanal ağı bağlayın.
**Yapılandırma sunucusu** | Tek bir tüm hello şirket içi Site Recovery bileşenlerini çalıştıran yönetim sunucusu (fiziksel sunucu veya VMware VM) şirket içi. Bunlar bir yapılandırma sunucusuna işlem sunucusu, ana hedef sunucusu içerir. | Merhaba yapılandırma sunucusu bileşeni şirket içi ve Azure arasındaki iletişimi düzenler ve veri çoğaltma işlemlerini yönetir.
 **İşlem sunucusu**  | Varsayılan olarak hello yapılandırma sunucusunda yüklü. | Çoğaltma ağ geçidi olarak davranır. Çoğaltma verilerini alıp, önbelleğe alma, sıkıştırma ve şifreleme iyileştirir ve tooAzure depolama gönderir.<br/><br/> Merhaba işlem sunucusu da hello Mobility hizmeti tooprotected makinelere göndermeli yüklemesini işler.<br/><br/> Ek ayrı adanmış işlem sunucular, birimler çoğaltması trafiğini artırma toohandle ekleyebilirsiniz.
 **Ana hedef sunucu** | Merhaba şirket içi yapılandırma sunucusu üzerinde varsayılan olarak yüklüdür. | Azure’dan yeniden çalışma sırasında çoğaltma verilerini işler.<br/><br/> Yeniden çalışma trafiğinin hacmi yüksekse, yeniden çalışma için ayrı bir ana hedef sunucu dağıtabilirsiniz.
**Çoğaltılmış sunucuları** | Merhaba Mobility hizmeti bileşeninin yüklü her Windows/Linux sunucusu üzerinde tooreplicate istiyor. El ile her makinede veya hello işlem sunucusu anında yüklemesinden ile yüklenebilir.
**İlk duruma döndürme** | Yeniden çalışma için bir VMware altyapı gereklidir. Geri tooa fiziksel sunucu kapatamazsınız.


**Şekil 1: Fiziksel tooAzure bileşenleri**

![Bileşenler](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Çoğaltma işlemi

1. Şirket içi ve Azure bileşenleri de dahil olmak üzere hello dağıtım, ayarlayın. Merhaba kurtarma Hizmetleri kasasına hello çoğaltma kaynak ve hedef hello yapılandırma sunucusunu ayarlamayı, bir çoğaltma ilkesi oluşturmak hello Mobility hizmeti dağıtmak, çoğaltmayı etkinleştirmek ve yük devretme testi çalıştırmak belirtin.
2.  Makinelerin çoğaltılacağı hello Çoğaltma İlkesi ve bir başlangıç kopyasını hello veri uygun olarak çoğaltılmış tooAzure Depolama ' dir.
4. İlk çoğaltma sonlandırıldıktan sonra delta değişiklikleri tooAzure çoğaltmasını başlar. Bir makine için izlenen değişiklikler bir .hrl dosyasında saklanır.
    - Çoğaltma HTTPS 443 numaralı bağlantı noktasında hello yapılandırma sunucusuyla gelen çoğaltma yönetimi için iletişim kurar.
    - Çoğaltılan makineler Gönder çoğaltma verileri toohello işlem sunucusu HTTPS 9443 bağlantı noktasına gelen (değiştirilmiş).
    - Merhaba yapılandırma sunucusu Azure ile çoğaltma yönetimi HTTPS 443 giden bağlantı noktası üzerinden düzenler.
    - Merhaba işlem sunucusu kaynak makinelerden verileri alan, en iyi duruma getirir ve bunu şifreler ve tooAzure depolama bağlantı noktası 443 üzerinden giden gönderir.
    - Çoklu VM tutarlılığını etkinleştirmek, ardından hello çoğaltma grubundaki birbiriyle 20004 bağlantı noktası üzerinden iletişim kurar. Çoklu VM, birden çok makineyi yük devrettikleri zaman kilitlenmeyle tutarlı ve uygulamayla tutarlı kurtarma noktalarını paylaşan çoğaltma grupları halinde gruplandırdığınızda kullanılır. Bu makineler çalışıyorsa yararlıdır hello aynı iş yükünü ve toobe tutarlı gerekir.
5. Trafiğidir çoğaltılmış tooAzure depolama ortak uç noktaları, üzerinde Internet hello. Alternatif olarak, Azure ExpressRoute [genel eşliğini](../expressroute/expressroute-circuit-peerings.md#public-peering) kullanabilirsiniz. Bir siteden siteye VPN bağlantısını bir şirket içi site tooAzure üzerinden trafik çoğaltma desteklenmiyor.

**Şekil 2: Fiziksel tooAzure çoğaltma**

![Gelişmiş](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Yük devretme ve yeniden çalışma işlemi

Yük devretme sınaması beklenen şekilde çalıştığını doğruladıktan sonra planlanmamış yük devretmeler tooAzure gerektiği gibi çalıştırabilirsiniz. Bir yük devretme çalıştırdığınızda, Azure Vm'leri çoğaltılmış verilerden oluşturulur. Birincil şirket içi sitenize yeniden kullanılabilir duruma geldiğinde, daha sonra geri yük devredebilir. Şunlara dikkat edin:

- Planlanan yük devretme desteklenmez.
- Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md), birden fazla makine birlikte üzerinden toofail.
- Bir yük devretme toostart erişilirken hello iş yükü Azure VM hello çoğaltmasından uygulayın.
- Merhaba birincil site yeniden kullanılabilir duruma geldiğinde, hello makine hello ikincil toohello birincil sitesinden çoğaltılır. Ardından, planlanmamış bir yük devretme hello ikincil siteden çalıştırma. Bu yük devretme yürüttükten sonra veri arka şirket içi olur ve yeniden tooenable çoğaltma tooAzure gerekir.

Yeniden çalışma bileşenleri şunları içerir:

- **Azure'da geçici işlem sunucusu**: bir Azure VM tooact bir işlem sunucusu olarak, Azure toohandle Çoğaltmada tooset gerekir. Yeniden çalışma sona erdikten sonra bu VM'yi silebilirsiniz.
- **VPN bağlantısı**: hello Azure ağ toohello şirket içi siteden bir VPN bağlantısı (veya Azure ExpressRoute) gerekir.
- **Ayrı şirket içi ana hedef sunucusu**: (Merhaba yapılandırma sunucusuna varsayılan olarak yüklenir) hello şirket içi ana hedef sunucusu yeniden çalışma işlemini yürütür. Geri büyük miktarda trafik başarısız olursa, bu amaçla bir ayrı şirket içi ana hedef sunucusu ayarlamanız gerekir.
- **Yeniden çalışma ilkesi**: geri dönme ilkesini gerekir. Bu ilke çoğaltma ilkenizi oluşturduğunuzda otomatik olarak oluşturulur.
- **VMware altyapı**: geri başarısız olması tooan şirket içi VMware VM. Şirket içi fiziksel sunucuların tooAzure çoğaltıyorsanız bile bu, bir şirket içi VMware altyapı ihtiyacınız anlamına gelir.

**Şekil 3: Fiziksel sunucuya geri dönme**

![Yeniden çalışma](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[2. adım: Önkoşullar ve sınırlamalar doğrulayın](physical-walkthrough-prerequisites.md)
