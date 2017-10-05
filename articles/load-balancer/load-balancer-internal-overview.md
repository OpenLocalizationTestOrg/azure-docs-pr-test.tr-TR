---
title: "İç yük dengeleyici genel bakış | Microsoft Docs"
description: "İç yük dengeleyici ve özellikleri için genel bakış. Bir yük dengeleyici iç uç noktalar yapılandırmak Azure ve olası senaryoları için nasıl çalışır?"
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
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a>İç yük dengeleyiciye genel bakış

Yük Dengeleyici Internet'e, iç yük dengeleyiciye (ILB) yalnızca bulut hizmeti ya da Azure altyapı erişmek için VPN kullanarak iç kaynaklara trafiğini yönlendirir. Böylece bunlar hiçbir zaman doğrudan bir Internet uç noktasına sunulur altyapı yük dengeli sanal IP adreslerine bir bulut hizmeti ya da bir sanal ağ (VIP) erişimi sınırlandırır. Bu, iç Azure'da çalıştırmak ve bulut içinde veya kaynakları şirket içi erişilen için iş kolu (LOB) uygulamaları sağlar.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Bir iç yük dengeleyici neden ihtiyacınız

Azure iç yük dengeleyici (ILB) Yük Dengeleme bir bulut hizmeti veya bölgesel kapsama sahip bir sanal ağ içinde bulunan sanal makineler arasında sağlar. Kullanım ve bölgesel kapsama sahip sanal ağ yapılandırması hakkında daha fazla bilgi için bkz: [bölgesel sanal ağlar](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) Azure Web günlüğündeki. Benzeşim grubu için yapılandırılmış mevcut sanal ağlar ILB’yi kullanamaz.

ILB Yük Dengeleme aşağıdaki türleri sağlar:

* Sanal makineler aynı bulut hizmetinde bulunan sanal makineler kümesi için bir bulut hizmetinden içinde (bkz: Şekil 1).
* (Bkz: Şekil 2) sanal aynı bulut hizmetinde bulunan sanal makineler kümesi için sanal ağdaki sanal makinelerden bir sanal ağ içindeki ağ.
* (Bkz: Şekil 3) şirket içi bilgisayarlardan sanal aynı bulut hizmetinde bulunan sanal makineler kümesi için şirket içi sanal ağ için ağ.
* Arka uç katmanları Internet'e değildir ancak Internet'e yönelik katmanından trafiği için Yük Dengeleme gerektiren Internet'e, çok katmanlı uygulamalar.
* Yük Dengeleme ek yük dengeleyici donanım veya yazılım gerektirmeden Azure üzerinde barındırılan LOB uygulamaları için. Şirket içi sunucular, trafik yükü olduğu bilgisayarları kümesinde dahil dengeli.

## <a name="internet-facing-multi-tier-applications"></a>Internet'e yönelik çok katmanlı uygulamalar

Web katmanı Internet istemciler için Internet'e yönelik uç noktalar vardır ve Yük Dengelemesi kümesinin bir parçası olur. Yük Dengeleyici web sunucularına TCP bağlantı noktası 443 (HTTPS) için web istemcilerinden gelen trafiği dağıtır.

Veritabanı sunucuları, web sunucuları için depolama alanı kullanan bir ILB uç nokta arkasındaki. ILB kümesindeki veritabanı sunucuları arasında dengeli trafiğidir uç nokta, bu veritabanı hizmeti yük dengeli.

Aşağıdaki görüntüde aynı bulut hizmetinde çok katmanlı uygulama Internet'e gösterir.

![İç Yük Dengeleme tek bulut hizmeti](./media/load-balancer-internal-overview/IC736321.png)

Şekil 1 - Internet'e yönelik çok katmanlı uygulama

ILB hizmet ILB için tüketen olandan farklı bir bulut hizmeti dağıtıldığında çok katmanlı bir uygulama için başka bir olası kullanılmasıdır.

ILB uç noktası aynı sanal ağ kullanarak bulut hizmetlerine erişebilir. Aşağıdaki resimde, ön uç web sunucusu farklı bir bulut hizmeti veritabanı arka uç ve ILB uç noktası aynı sanal ağda kullanarak olduğundan gösterir.

![İç Yük Dengeleme bulut hizmetleri arasında](./media/load-balancer-internal-overview/IC744147.png)

Şekil 2 - farklı bir bulut hizmeti ön uç sunucuları

## <a name="intranet-line-of-business-applications"></a>İntranet iş kolu uygulamaları

Şirket içi ağda istemcilerinden gelen trafiği almak Azure ağı için VPN bağlantısını kullanarak iş KOLU sunucuları arasında Yük Dengelemesi.

İstemci makine erişimine, noktasını site VPN kullanarak Azure VPN hizmetinden bir IP adresine sahip olur. ILB uç nokta barındırılan LOB uygulaması kullanımına izin verir.

![Noktası site VPN kullanarak iç Yük Dengeleme](./media/load-balancer-internal-overview/IC744148.png)

Şekil 3 - LB bitiş noktasının ardındaki barındırılan LOB uygulamaları

Başka bir senaryo için LOB ILB uç nokta yapılandırıldığı sanal ağ için siteden siteye VPN olmalıdır. Bu, şirket içi ağ trafiğini ILB uç noktasına yönlendirilmesini sağlar.

![Siteden siteye VPN kullanarak iç Yük Dengeleme](./media/load-balancer-internal-overview/IC744150.png)

Şekil 4 - ILB uç noktasına yönlendirilen şirket içi ağ trafiği

## <a name="limitations"></a>Sınırlamalar

İç yük dengeleyici yapılandırmalarının SNAT desteklemez. Bu belge bağlamında, bağlantı noktası maskelenmiş kaynak ağ adresi çevirisi için SNAT başvuruyor.  Burada ilgili iç yük dengeleyicinin ön uç IP adresi ulaşmak için bir VM'de yük dengeleyici havuzu gerekiyor senaryoları için geçerlidir. Bu senaryo için iç yük dengeleyici desteklenmiyor. Bağlantı hataları Akış akış kaynaklanan VM dengelendiği olduğunda meydana gelir. Bir proxy stili yük dengeleyici gibi senaryolar için kullanmanız gerekir.

## <a name="next-steps"></a>Sonraki Adımlar

[Azure yük dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md)

[Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama](load-balancer-get-started-internet-arm-ps.md)

[Bir iç yük dengeleyici yapılandırma kullanmaya başlama](load-balancer-get-started-ilb-arm-ps.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
