---
title: "aaaAzure ağ | Microsoft Docs"
description: "Azure ağ hizmetlerini ve özellikleri hakkında bilgi edinin."
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Azure ağı

Azure birlikte veya ayrı olarak kullanılan ağ yeteneklerini çeşitli sağlar. Aşağıdaki temel işlevler toolearn bunları hakkında daha fazla hello birini tıklatın:
- [Azure kaynakları arasında bağlantı](#connectivity): bağlanmak Azure kaynaklarına güvenli, özel bir sanal ağ hello bulutta bir araya.
- [Internet bağlantısı](#internet-connectivity): Azure kaynaklarından tooand hello Internet iletişim kurar.
- [Şirket içi bağlantı](#on-premises-connectivity): adanmış bağlantı tooAzure veya hello Internet üzerinden sanal özel ağ (VPN) üzerinden bir şirket içi ağ tooAzure kaynaklarına bağlanın.
- [Yük Dengeleme ve trafik yönü](#load-balancing): Yük Dengeleme trafik tooservers hello aynı konuma ve farklı konumlarda doğrudan trafiği tooservers.
- [Güvenlik](#security): ağ alt ağları veya tek tek sanal makineler (VM) arasındaki ağ trafiğini filtre.
- [Yönlendirme](#routing): veya tam denetim Azure ve şirket kaynaklarınız arasında yönlendirme varsayılan yönlendirme kullanma.
- [Yönetilebilirlik](#manageability): izleme ve Azure ağ kaynaklarınızı yönetin.
- [Dağıtım ve yapılandırma araçları](#tools): bir web tabanlı portal veya platformlar arası komut satırı araçları toodeploy kullanın ve ağ kaynaklarını yapılandırın.

## <a name="Connectivity"></a>Azure kaynakları arasında bağlantı

Sanal makineler, bulut Hizmetleri, sanal makine ölçek kümeleri ve Azure App Service ortamları gibi Azure kaynakları özel olarak birbirleri ile bir Azure sanal ağı (VNet) iletişim kurabilir. Bir VNet hello ayrılmış Azure bulut tooyour mantıksal yalıtımının olan [abonelik](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json). Her Azure aboneliği içindeki birden çok sanal ağlar ve Azure uygulayabilirsiniz [bölge](https://azure.microsoft.com/regions). Her sanal ağ, diğer sanal ağlardan yalıtılır. Her sanal ağ için şunları yapabilirsiniz:

- Ortak ve özel (RFC 1918) adreslerini kullanarak özel bir özel IP adres alanını belirtin. Azure kaynakları bağlı toohello VNet hello adres alanından atadığınız özel bir IP adresi atar.
- Bir veya daha fazla alt ağ içinde Hello VNet segmentlere ayırmak ve hello sanal adres alanı tooeach alt kısmı paylaştırabilirsiniz.
- Azure tarafından sağlanan ad çözümlemesi kullanın veya kaynaklar tarafından kullanılmak üzere kendi DNS sunucusu tooa VNet bağlı belirtin.

Merhaba okuma hello Azure sanal ağ hizmeti hakkında daha fazla toolearn [sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi. Sanal ağlar tooeach diğer bağlanabilir, kaynakları etkinleştirme tooeither VNet toocommunicate birbirleri ile sanal ağlar bağlanır. Veya her ikisini seçenekleri tooconnect sanal ağlar tooeach diğer aşağıdaki hello kullanabilirsiniz:

- **Eşliği:** etkinleştirir kaynaklara bağlı hello içinde toodifferent Azure Vnet birbiriyle aynı Azure bölgesinde toocommunicate. Merhaba kaynaklara bağlı toohello değilmiş gibi hello bant genişliği ve gecikme hello olup Vnet'ler arasında aynı hello aynı sanal ağı. eşleme, hakkında daha fazla toolearn okuma hello [sanal ağ eşleme genel bakış](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **VPN ağ geçidi:** etkinleştirir kaynaklara bağlı toodifferent Azure sanal ağlar farklı Azure bölgeleri toocommunicate içinde birbiriyle. Sanal ağlar arasındaki trafik bir Azure VPN ağ geçidi üzerinden akar. Sanal ağlar arasında bant genişliği sınırlı toohello bant genişliği hello ağ geçidi ' dir. bir hello okuma ile VPN ağ geçidi, sanal ağlara bağlanma hakkında daha fazla toolearn [bölgeler arasında VNet-VNet bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

## <a name="internet-connectivity"></a>Internet bağlantısı

Tüm Azure kaynaklarına bağlı tooa VNet varsayılan giden bağlantı toohello Internet vardır. Merhaba özel IP adresi hello kaynağının kaynak ağ adresi (SNAT) tooa genel IP adresi hello Azure altyapısı tarafından çevrilen değil. toolearn hello okuma giden Internet bağlantısı hakkında daha fazla [azure'da giden bağlantılar anlama](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

toocommunicate Internet SNAT, bir kaynak olmadan genel bir IP adresi atanmalıdır hello Internet ya da toocommunicate giden toohello tooAzure kaynaklardan gelen. Merhaba okuma genel IP adresleri hakkında daha fazla toolearn [ortak IP adresleri](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

## <a name="on-premises-connectivity"></a>Şirket içi bağlantısı

Kaynaklar, sanal ağınızda güvenli bir şekilde bir VPN bağlantısı veya doğrudan özel bir bağlantı erişebilirsiniz. Azure sanal ağınıza ve şirket içi ağınız arasında ağ trafiğini toosend, bir sanal ağ geçidi oluşturmanız gerekir. Merhaba ağ geçidi toocreate hello bağlantı türü için kullanmak istediğiniz VPN veya ExpressRoute ayarlarını yapılandırın.

Şirket içi ağ tooa seçenekleri aşağıdaki hello herhangi bir bileşimini kullanarak VNet bağlanabilir:

**Noktadan siteye (VPN üzerinden SSTP)**

Resim aşağıdaki hello birden çok bilgisayar ve bir sanal ağ arasında ayrı noktası toosite bağlantılarını gösterir:

![Noktadan siteye](./media/networking-overview/point-to-site.png)

Bu bağlantı tek bir bilgisayar ve bir sanal ağ arasında kurulur. Çok az kayıpla veya hiç değişiklik tooyour mevcut ağ gerektirdiğinden bu bağlantı türü, yalnızca Azure ile ya da geliştiricileri için başlıyorsanız mükemmeldir. Ayrıca bir konferans gibi uzak bir konumdan bağlanırken kullanışlı veya giriş. Noktadan siteye bağlantıları genellikle hello yoluyla siteden siteye bağlantı ile birlikte aynı sanal ağ geçidi. Merhaba bağlantı hello SSTP Protokolü şifrelenmiş tooprovide iletişimi hello bilgisayarla hello VNet arasında hello Internet üzerinden kullanır. bir noktadan siteye VPN için hello gecikme Hello trafiğin hello Internet geçeceğini öngörülemeyen, taşımaktadır.

**Siteden siteye (IPSec/IKE VPN tüneli)**

![Siteden siteye](./media/networking-overview/site-to-site.png)

Bu bağlantı, şirket içi VPN aygıtınızın ve bir Azure VPN ağ geçidi arasında kurulur. Bu bağlantı türü tooaccess hello VNet yetkilendirmek herhangi bir şirket içi kaynak sağlar. Merhaba, şirket içi cihaz hello Azure VPN ağ geçidi arasındaki hello Internet üzerinden şifrelenmiş iletişimi sağlayan bir IPSec/IKE VPN bağlantısıdır. Birden çok şirket içi siteler toohello bağlanabilir aynı VPN ağ geçidi. Merhaba içi bağlı her sitede VPN cihazı bir NAT'nin arkasına olmayan bir dışarıya yönelik genel IP adresi olmalıdır siteden siteye bağlantı hello gecikme Hello trafiğin hello Internet geçeceğini öngörülemeyen, taşımaktadır.

**ExpressRoute (adanmış özel bağlantı)**

![ExpressRoute](./media/networking-overview/expressroute.png)

Bu tür bir bağlantı ağınız ve Azure arasında bir ExpressRoute iş ortağı üzerinden kurulur. Bu bağlantı özeldir. Trafik hello Internet erişmez. ExpressRoute bağlantısı için hello gecikme süresini tahmin edilebilir, olduğu hello Internet trafiği çapraz geçiş değil. ExpressRoute ile bir siteden siteye bağlantı birleştirilebilir.

Merhaba okuma tüm hello önceki bağlantı seçenekleri hakkında daha fazla toolearn [bağlantı topoloji diyagramları](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

## <a name="load-balancing"></a>Yük Dengeleme ve trafik yönü

Microsoft Azure, birden çok ağ trafiğini nasıl dağıtıldığını yönetmek için hizmetleri ve Yük Dengeleme sağlar. Özellikleri ayrı ayrı veya birlikte aşağıdaki hello birini kullanabilirsiniz:

**DNS Yük Dengeleme**

Hello Azure trafik Yöneticisi hizmeti, Genel DNS Yük Dengeleme sağlar. Trafik Yöneticisi tooclients yönlendirme yöntemleri aşağıdaki hello birini temel alarak sağlıklı bir uç noktanın hello IP adresiyle yanıt verir:
- **Coğrafi:** istemcileri yönlendirilmiş toospecific uç noktaları (Azure, dış veya iç içe) tabanlı DNS sorgularını hangi coğrafi konum kaynaklanan. Bu yöntem, bir istemcinin coğrafi bölge bilerek ve bunları temel alan yönlendirme önemli olduğu senaryolara olanak sağlar. Örnek veri egemenliği gerektirir, içerik & kullanıcı deneyiminin yerelleştirme uymaktan ve farklı bölgelerdeki trafiğini ölçme verilebilir.
- **Performans:** başlangıç IP adresi döndürülmezse toohello istemci hello "en yakın" toohello istemci. Merhaba 'en yakın' bitiş noktası tarafından coğrafi uzaklığı ölçülen mutlaka yakın değil. Bunun yerine, bu yöntem, ağ gecikmesi ölçerek hello en yakın endpoint belirler. Trafik Yöneticisi bir Internet gecikme tablo tootrack hello gidiş dönüş süresi IP adresi aralıkları ve her Azure veri merkezi arasında tutar.
- **Öncelik:** trafiğidir yönlendirilmiş toohello birincil (en yüksek öncelik) uç noktası. Merhaba birincil uç noktası kullanılabilir durumda değilse, trafik Yöneticisi yollar trafiği toohello ikinci uç nokta hello. Her iki hello birincil ve ikincil uç noktaları mevcut değilse hello trafiği toohello gider üçüncü, vb.. (Etkin veya devre dışı) yapılandırılmış hello durumuna göre hello uç noktasının kullanılabilirliğini ve devam eden uç nokta izleme hello.
- **Ağırlıklı hepsini:** her istek için trafik Yöneticisi kullanılabilir uç nokta rastgele seçer. bir uç noktasını hello olasılığını tooall kullanılabilir uç noktaları atanan hello ağırlıklarını temel alır. Hello kullanarak aynı bir bile trafik dağılımı tüm uç noktaları sonuçlarında arasında ağırlık. Daha yüksek veya düşük ağırlıkları üzerinde belirli uç noktalarını kullanarak fazla veya az sık hello DNS yanıtları döndürülen bu uç noktaları toobe neden olur.

Resim aşağıdaki hello bir web uygulaması yönlendirilmiş tooa Web uygulaması uç noktası için bir istek gösterir. Uç noktaları, sanal makineleri gibi diğer Azure hizmetlerine ve bulut hizmetlerini de olabilir.

![Traffic Manager](./media/networking-overview/traffic-manager.png)

Merhaba istemci toothat uç noktası doğrudan bağlanır. Bir uç nokta sağlıksız olduğunu ve istemcilerin tooa farklı, sağlıklı uç nokta yönlendiren azure trafik Yöneticisi algılar. Daha fazla trafik hello okuma Yöneticisi hakkında toolearn [Azure trafik Yöneticisi'ne genel bakış](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

**Uygulama yük dengeleme**

Hello Azure uygulama ağ geçidi hizmeti uygulama teslim denetleyicisi (ADC) bir hizmet olarak sağlar. Uygulama ağ geçidi çeşitli katman 7 (HTTP/HTTPS) Yük Dengeleme yeteneklerini bir web uygulaması da dahil olmak üzere, uygulamalarınız için web uygulamalarınızdan Güvenlik Açıkları ve güvenlik açıklarına tooprotect güvenlik duvarı sunar. Uygulama ağ geçidi toooptimize web grubu üretkenlik CPU-yoğun SSL sonlandırma toohello uygulama ağ geçidi boşaltarak sağlar. 

Diğer katman 7 Yönlendirme yetenekleri hepsini dağıtım gelen trafiği, tanımlama bilgisi tabanlı oturum benzeşimi, URL yolu tabanlı Yönlendirme ve hello özelliği toohost tek bir uygulama ağ geçidi arkasında birden çok Web siteleri içerir. Uygulama ağ geçidi, bir Internet'e dönük ağ geçidi, bir yalnızca iç ağ geçidi veya her ikisinin birleşimini yapılandırılabilir. Tam Azure uygulama ağ geçidi yönetilen, ölçeklenebilir ve yüksek oranda kullanılabilir. Daha iyi yönetilebilirlik için zengin tanılama ve günlüğe kaydetme özellikleri sağlar. Merhaba okuma uygulama ağ geçidi hakkında daha fazla toolearn [uygulama ağ geçidi'ne genel bakış](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

Merhaba aşağıdaki resimde URL yolu tabanlı uygulama ağ geçidi ile yönlendirme gösterir:

![Application Gateway](./media/networking-overview/application-gateway.png)

**Ağ yük dengeleme**

Hello Azure yük dengeleyici için tüm UDP ve TCP protokollerini yüksek performanslı, düşük gecikme süreli katman 4 Yük Dengeleme sağlar. Gelen ve giden bağlantılara yönetir. Genel ve iç yük dengeli uç noktalarını yapılandırabilirsiniz. Kuralları toomap tanımlayabilirsiniz gelen bağlantıları tooback uç havuzu hedefleri TCP ve HTTP sistem durumu yoklama seçenekleri toomanage hizmet kullanılabilirliği kullanarak. Yük Dengeleyici, hello okuma hakkında daha fazla toolearn [yük dengeleyici genel bakış](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

Resim aşağıdaki hello hem dış ve iç yük dengeleyici kullanan bir Internet'e yönelik çok katmanlı uygulama gösterir:

![Yük dengeleyici](./media/networking-overview/load-balancer.png)

## <a name="security"></a>Güvenlik

Seçenekler aşağıdaki hello kullanarak Azure kaynaklardan gelen trafiği tooand filtreleyebilirsiniz:

- **Ağ:** Azure ağ güvenlik gruplarını (Nsg'ler) toofilter gelen ve giden uygulayabilirsiniz trafiği tooAzure kaynakları. Her NSG bir veya daha fazla gelen ve giden kurallarını içerir. Her kural hello kaynak IP adresleri, hedef IP adresleri, bağlantı noktası ve trafiği ile filtrelenmiş Protokolü belirtir. Nsg'ler uygulanan tooindividual alt ağları ve tek tek sanal makineleri olabilir. Merhaba okuma Nsg'ler hakkında daha fazla toolearn [ağ güvenlik gruplarını genel bakış](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **Uygulama:** web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi'ni kullanarak, web uygulamalarınızı güvenlik açıkları ve güvenlik açıklarına koruyabilirsiniz. SQL ekleme saldırıları, siteler arası komut dosyası ve hatalı biçimlendirilmiş üstbilgiler ortak örnek verilebilir. Uygulama ağ geçidi Bu trafik çıkış filtreleri ve web sunucularına ulaşması durdurur. Hangi kuralları etkinleştirilmiş istediğiniz mümkün tooconfigure şunlardır. Merhaba özelliği tooconfigure SSL anlaşma ilkeleri ilkeler toobe devre dışı belirli tooallow sağlanır. Merhaba okuma hello web uygulaması Güvenlik Duvarı hakkında daha fazla toolearn [Web uygulaması güvenlik duvarı](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

Azure olmayan sağlayın veya toouse Ağ uygulamalarının şirket içi kullanmak istediğiniz ağ özelliğini gerekiyorsa, Vm'lerde hello ürünleri uygulamak ve bunları tooyour VNet bağlayın. Merhaba [Azure Marketi](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) birkaç farklı VM şu anda kullanabilir ağ uygulamaları ile önceden yapılandırılmış içerir. Bu önceden yapılandırılmış sanal makineleri genellikle başvurulan tooas ağ sanal Gereçleri (NVA) var. NVAs, güvenlik duvarı ve WAN iyileştirmesi gibi uygulamalar ile kullanılabilir.

## <a name="routing"></a>Yönlendirme

Azure varsayılan kaynakları bağlı tooany alt ağdaki tüm VNet toocommunicate birbirleriyle etkinleştirmek yönlendirme tabloları oluşturur. Ya da uygulayabilir veya şu rotaları toooverride türlerini hello her ikisi de Azure oluşturduğu varsayılan yolların hello:
- **Kullanıcı tanımlı:** özel yol tablolarını her alt ağ trafiği yönlendirilmiş toofor olduğu denetleyen yollar oluşturabilirsiniz. Merhaba okuyun, kullanıcı tanımlı yollar hakkında daha fazla toolearn [kullanıcı tanımlı yollar](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **Sınır Ağ Geçidi Protokolü (BGP):** bir Azure VPN ağ geçidi veya ExpressRoute bağlantısı kullanarak VNet tooyour şirket içi ağınıza bağlanıyorsanız, BGP yolları tooyour sanal ağlar yayabilirsiniz. BGP hello Internet tooexchange Yönlendirme ve ulaşılabilirlik bilgilerini iki veya daha fazla ağ arasında yaygın olarak kullanılan hello standart yönlendirme protokolüdür. Azure sanal ağlar, BGP etkinleştirir hello Azure VPN ağ geçitleri ve şirket içi VPN cihazlarınızı Hello bağlamında kullanıldığında çağrılan BGP eşleri veya Komşuları olarak tooexchange "Merhaba kullanılabilirliği ve ulaşılabilirliği bu önekler için her iki ağ geçidini bildiren yolları" Merhaba ağ geçitlerinden veya yönlendiricilerden söz konusu aracılığıyla toogo. BGP, bir BGP eş tooall bir BGP ağ geçidinin öğrendiği yolları yayarak birden fazla ağ arasında geçiş yönlendirme de etkinleştirebilir diğer BGP eşleri. BGP hakkında daha fazla toolearn bkz hello [BGP Azure VPN ağ geçidi'ne genel bakış ile](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

## <a name="manageability"></a>Yönetilebilirlik

Azure hello aşağıdaki toomonitor araçları ve ağ yönetmek sağlar:
- **Etkinlik günlükleri:** tüm Azure kaynaklarınız gerçekleştirilen işlemler hakkında bilgi sağlayan etkinlik günlükleri yerleştirin, işlem durumunu ve kimin başlattığını hello işlemi. Merhaba okuyun, etkinlik günlükleri hakkında daha fazla toolearn [etkinlik günlükleri genel bakış](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **Tanılama günlüklerini:** Periyodik ve spontaneous olayları ağ kaynakları tarafından oluşturulan ve Azure depolama hesaplarında oturum, tooan Azure olay hub'ı gönderilen veya tooAzure günlük analizi gönderilir. Tanılama günlüklerini Insight toohello sistem durumunu bir kaynak sağlayın. Tanılama günlükleri, yük dengeleyici (Internet'e yönelik), ağ güvenlik grupları, yol ve uygulama ağ geçidi için sağlanır. Tanılama günlükleri, hello okuma hakkında daha fazla toolearn [tanılama günlükleri'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **Ölçümler:** ölçümleri performans ölçümleri ve kaynakları bir süre boyunca toplanan sayaçları verilmiştir. Ölçümleri eşiklere dayanarak kullanılan tootrigger uyarıları olabilir. Şu anda ölçümleri uygulama ağ geçidinde bulunmaktadır. Merhaba okuma ölçümler hakkında daha fazla toolearn [ölçümleri genel bakış](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **Sorun giderme:** sorun giderme bilgileri doğrudan hello Azure portal ' erişilebilir. Merhaba bilgiler ExpressRoute, VPN ağ geçidi, uygulama ağ geçidi, ağ güvenlik günlükleri, yollar, DNS, yük dengeleyici ve trafik Yöneticisi ile ortak sorunları tanılamanıza yardımcı olur.
- **Rol tabanlı erişim denetimi (RBAC):** kimin oluşturabilir ve rol tabanlı erişim denetimi (RBAC) ile ağ kaynaklarını yönetme. Merhaba okuyarak RBAC hakkında daha fazla bilgi [RBAC ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi. 
- **Paket yakalama:** hello Azure ağ hizmeti sağlar İzleyicisi Merhaba bir paket yakalama hello VM içinde bir uzantısı aracılığıyla bir VM'de yeteneği toorun. Bu özellik, Linux ve Windows VM'ler için kullanılabilir. Paket yakalama, hello okuma hakkında daha fazla toolearn [paket yakalama genel bakış](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **IP akışları doğrulayın:** Ağ İzleyicisi vermediğini, tooverify IP akışlarının bir Azure VM ve uzak kaynak toodetermine arasında paketlerin izin verilen veya reddedilen. Bu yetenek Yöneticiler hello yeteneği sağlar. tooquickly bağlantı sorunları tanılayın. toolearn nasıl tooverify IP akışlar hakkında daha fazla okuma hello [IP akış doğrulayın genel bakış](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **VPN bağlantı sorunlarını giderme:** özelliği tooquery bir bağlantı veya ağ geçidi hello ve hello kaynakları hello durumunu doğrulamak hello Ağ İzleyicisi VPN sorun gidericisini yeteneğini sağlar. VPN bağlantıları hello okuyun, sorun giderme hakkında daha fazla toolearn [sorun giderme genel bakış VPN bağlantısı](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makale.
- **Ağ topolojisi görüntüleyin:** hello ağ kaynaklarına grafik gösterimi Ağ İzleyicisi sahip bir VNet görüntüleyin. Ağ topolojisi, hello okuma görüntüleme hakkında daha fazla toolearn [topolojisine genel bakış](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.

## <a name="tools"></a>Dağıtım ve yapılandırma araçları

Dağıtma ve Azure ağ kaynaklarını araçları aşağıdaki hello birini yapılandırın:

- **Azure portal:** bir tarayıcıda çalışan bir grafik kullanıcı arabirimi. Açık hello [Azure portal](http://portal.azure.com).
- **Azure PowerShell:** Azure Windows bilgisayarları yönetmek için komut satırı araçları. Azure PowerShell hakkında daha fazla okuma hello tarafından bilgi [Azure PowerShell genel bakış](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **Azure komut satırı arabirimi (CLI):** Azure Linux, macOS ya da Windows bilgisayarları yönetmek için komut satırı araçları. Okuma hello tarafından hello Azure CLI hakkında daha fazla bilgi [Azure CLI genel bakış](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- **Azure Resource Manager şablonları:** hello altyapısı ve Azure çözümünü yapılandırmasını tanımlayan bir dosyada (JSON biçiminde). Bir şablon kullanarak çözümünü yaşam döngüsü boyunca defalarca dağıtabilir ve kaynaklarınızın tutarlı bir durumda dağıtıldığından emin olabilirsiniz. Şablonları hello okuma, yazma hakkında daha fazla toolearn [en iyi uygulamalar şablonları oluşturmak için](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi. Şablonları hello ile Azure portal, CLI veya PowerShell dağıtılabilir. şablonlarla hemen çalışmaya tooget dağıtmak hello birini hello birçok önceden yapılandırılmış şablonlarında [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/?term=network) kitaplığı. 

## <a name="pricing"></a>Fiyatlandırma

Bazı başkalarının özgürlüğüne sahip olmanıza rağmen hello Azure ' bir ücret Ağ Hizmetleri sahip. Görünüm hello [sanal ağ](https://azure.microsoft.com/pricing/details/virtual-network), [VPN ağ geçidi](https://azure.microsoft.com/pricing/details/vpn-gateway), [uygulama ağ geçidi](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [yük dengeleyici](https://azure.microsoft.com/pricing/details/load-balancer), [Ağ İzleyicisi](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [trafik Yöneticisi](https://azure.microsoft.com/pricing/details/traffic-manager) ve [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) sayfalar daha fazla bilgi için fiyatlandırma.

## <a name="next-steps"></a>Sonraki adımlar

- İlk sanal ağınızı oluşturmak ve hello hello adımları tamamlayarak birkaç VM'ler tooit bağlanmak [ilk sanal ağınızı oluşturmak](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- Merhaba hello adımları izleyerek, bilgisayar tooa VNet bağlantı [noktadan siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
- Yük Dengelemesi Internet trafiği toopublic sunucuları hello hello adımları tamamlayarak [bir Internet'e yönelik Yük Dengeleyici oluşturma](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) makalesi.
