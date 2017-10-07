---
title: "aaaInternal yük dengeleyici genel bakış | Microsoft Docs"
description: "İç yük dengeleyici ve özellikleri için genel bakış. Bir yük dengeleyici Azure ve olası senaryolar için tooconfigure iç uç noktaları nasıl çalışır?"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>İç yük dengeleyiciye genel bakış

Merhaba Internet'e yönelik Yük Dengeleyici, hello iç yük dengeleyiciye (ILB) trafiği yalnızca tooresources hello bulut hizmeti veya VPN tooaccess hello Azure altyapı kullanarak içinde yönlendirir. böylece hiçbir zaman doğrudan gösterilen tooan Internet uç noktası olmaz hello altyapı erişim toohello yük dengeli sanal IP adresleri (VIP) bir bulut hizmeti ya da bir sanal ağ kısıtlar. Bu iş (LOB) uygulamaları toorun Azure iç satırının sağlar ve hello bulut içinde veya kaynakları şirket içi erişilen.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Bir iç yük dengeleyici neden ihtiyacınız

Azure iç yük dengeleyici (ILB) Yük Dengeleme bir bulut hizmeti veya bölgesel kapsama sahip bir sanal ağ içinde bulunan sanal makineler arasında sağlar. Merhaba kullanın ve bölgesel kapsama sahip sanal ağ yapılandırması hakkında daha fazla bilgi için bkz: [bölgesel sanal ağlar](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) hello Azure blogu içinde. Benzeşim grubu için yapılandırılmış mevcut sanal ağlar ILB’yi kullanamaz.

ILB hello şu Yük Dengelemesi türlerini sağlar:

* Bir bulut hizmetinde hello içinde bulunan sanal makinelerin sanal makineleri tooa kümesinden aynı bulut hizmeti (bkz: Şekil 1).
* Bir sanal ağ içindeki sanal makinelerden hello sanal ağ tooa kümesi içinde hello duran sanal makineleri aynı sanal Merhaba, bulut hizmeti (bkz: Şekil 2) ağ.
* Bir şirket içi sanal ağ için şirket içi bilgisayarları tooa kümesinden hello içinde bulunan sanal makineleri aynı sanal Merhaba, bulut hizmeti (bkz: Şekil 3) ağ.
* Merhaba arka uç katmanları Internet'e değildir ancak gerektirir Internet'e, çok katmanlı uygulamalar hello Internet'e katmanından trafiği için Dengeleme yükler.
* Yük Dengeleme ek yük dengeleyici donanım veya yazılım gerektirmeden Azure üzerinde barındırılan LOB uygulamaları için. Şirket içi sunucular, trafik yükü olduğu bilgisayarları hello kümesinde dahil dengeli.

## <a name="internet-facing-multi-tier-applications"></a>Internet'e yönelik çok katmanlı uygulamalar

Merhaba web katmanı Internet istemciler için Internet'e yönelik uç noktalar vardır ve Yük Dengelemesi kümesinin bir parçası olur. Merhaba yük dengeleyici TCP bağlantı noktası 443 (HTTPS) toohello web sunucuları için web istemcilerinden gelen trafiği dağıtır.

Merhaba veritabanı hello web sunucuları için depolama alanı kullanan bir ILB uç nokta arkasında sunucularıdır. Hangi trafiğidir hello ILB kümesindeki hello veritabanı sunucuları arasında dengeli uç nokta, bu veritabanı hizmeti yük dengeli.

Görüntü gösterir aşağıdaki hello hello çok katmanlı uygulama Internet'e hello içinde aynı bulut hizmeti.

![İç Yük Dengeleme tek bulut hizmeti](./media/load-balancer-internal-overview/IC736321.png)

Şekil 1 - Internet'e yönelik çok katmanlı uygulama

Merhaba ILB hello ILB için bir alıcı hello hizmet hello daha tooa farklı bir bulut hizmeti dağıtıldığında çok katmanlı bir uygulama için başka bir olası kullanılmasıdır.

Bulut Hizmetleri aynı sanal ağ olacaktır hello kullanarak erişim toohello ILB uç noktası. ön uç web sunucuları hello veritabanı arka uç farklı bir bulut hizmetinden içinde görüntü görülmektedir izleyerek ve kullanarak hello hello ILB uç nokta hello içinde aynı sanal ağ.

![İç Yük Dengeleme bulut hizmetleri arasında](./media/load-balancer-internal-overview/IC744147.png)

Şekil 2 - farklı bir bulut hizmeti ön uç sunucuları

## <a name="intranet-line-of-business-applications"></a>İntranet iş kolu uygulamaları

Merhaba şirket ağındaki istemcilerinden gelen trafiği VPN bağlantısı tooAzure ağ kullanarak LOB sunucularını hello kümesi boyunca alın yük dengeli.

Merhaba istemci makine noktası toosite VPN kullanarak Azure VPN hizmetinden erişim tooan IP adresi gerekir. Hello kullan hello hello ILB uç barındırılan LOB uygulaması sağlar.

![İç Yük Dengeleme noktası toosite VPN kullanarak](./media/load-balancer-internal-overview/IC744148.png)

Şekil 3 - hello LB bitiş noktasının ardındaki barındırılan LOB uygulamaları

Başka bir hello LOB toohave hello ILB uç nokta yapılandırıldığı bir site toosite VPN toohello sanal ağ senaryodur. Bu, şirket içi ağ trafiği yönlendirilen toobe toohello ILB uç noktası sağlar.

![İç Yük Dengeleme site toosite VPN kullanma](./media/load-balancer-internal-overview/IC744150.png)

Şekil 4 - şirket içi ağ trafiğini yönlendirilen toohello ILB uç noktası

## <a name="limitations"></a>Sınırlamalar

İç yük dengeleyici yapılandırmalarının SNAT desteklemez. Bu belge Hello bağlamda SNAT tooport maskelenmiş kaynak ağ adresi çevirisi başvurur.  Bu, burada bir VM'de yük dengeleyici havuzuna tooreach hello ilgili iç yük dengeleyicinin ön uç IP adresi gerekiyor tooscenarios geçerlidir. Bu senaryo için iç yük dengeleyici desteklenmiyor. Bağlantı hataları Hello akış yükü dengelenmiş toohello hello akış kaynaklanan VM olduğunda meydana gelir. Bir proxy stili yük dengeleyici gibi senaryolar için kullanmanız gerekir.

## <a name="next-steps"></a>Sonraki Adımlar

[Azure yük dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md)

[Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama](load-balancer-get-started-internet-arm-ps.md)

[Bir iç yük dengeleyici yapılandırma kullanmaya başlama](load-balancer-get-started-ilb-arm-ps.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
