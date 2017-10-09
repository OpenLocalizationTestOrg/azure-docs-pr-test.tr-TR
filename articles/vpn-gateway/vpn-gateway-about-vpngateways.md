---
title: "VPN ağ geçidi genel bakış: şirket içi VPN bağlantıları tooAzure sanal ağlar oluşturun. | Microsoft Docs"
description: "Bu VPN ağ geçidi genel bakış hello yolları tooconnect tooAzure sanal ağlar hello Internet bir VPN bağlantısı kullanarak açıklanmaktadır. Temel bağlantı yapılandırmaları da buraya eklenmiştir."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>VPN Gateway hakkında

Bir VPN ağ geçidi, bir ortak bağlantı tooan arasında şifrelenmiş trafik içi konumu gönderir sanal ağ geçidi türüdür. Hello Microsoft ağ üzerinden Azure sanal ağlar arasında VPN ağ geçitleri şifrelenmiş toosend trafiği de kullanabilirsiniz. Azure sanal ağınıza ve şirket içi sitenizi arasındaki ağ trafiğini şifrelenmiş toosend, sanal ağınız için bir VPN ağ geçidi oluşturmanız gerekir.

Her bir sanal ağı yalnızca bir VPN ağ geçidi olabilir, ancak, birden çok bağlantı toohello oluşturabilirsiniz aynı VPN ağ geçidi. Çok Siteli bağlantı yapılandırması bunun bir örneğidir. Birden çok bağlantı toohello oluşturduğunuzda aynı VPN ağ geçidi, hello ağ geçidi için kullanılabilir paylaşım hello bant genişliği noktadan siteye VPN'lerde dahil tüm VPN tünelleri.

### <a name="whatis"></a>Sanal ağ geçidi nedir?

Bir sanal ağ geçidi iki oluşur veya daha fazla sanal makineleri hello GatewaySubnet adlı tooa belirli alt dağıtılabilir. Merhaba GatewaySubnet hello sanal ağ geçidi oluşturduğunuzda oluşturulur hello bulunan VM'ler. Sanal ağ geçidi VMs yapılandırılmış toocontain yönlendirme tabloları ve ağ geçidi Hizmetleri belirli toohello ağ geçidi verilmiştir. Merhaba hello sanal ağ geçidi parçası olan sanal makineleri doğrudan yapılandıramazsınız ve ek kaynaklar toohello GatewaySubnet hiçbir zaman dağıtmanız gerekir.

Merhaba ağ geçidi türü 'Vpn' kullanarak bir sanal ağ geçidi oluşturduğunuzda, belirli bir trafik şifreler sanal ağ geçidi türünü oluşturur; bir VPN ağ geçidi. Bir VPN ağ geçidi too45 dakika toocreate alabilir. Bu hello VM'ler hello VPN ağ geçidi bırakılıyor çünkü dağıtılan toohello GatewaySubnet ve belirttiğiniz hello ayarlarıyla yapılandırılır. Merhaba, seçtiğiniz ağ geçidi SKU'su VM'ler ne kadar güçlü hello belirler.

## <a name="gwsku"></a>Ağ Geçidi SKU'ları

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>VPN Gateway yapılandırma

VPN ağ geçidi bağlantısı belirli ayarlarla yapılandırılmış birden fazla kaynağı kullanır. Bazı durumlarda belirli bir sırada yapılandırılmalıdır rağmen hello kaynakların çoğunu ayrı olarak yapılandırılabilir.

### <a name="settings"></a>Ayarlar

Her kaynak için seçtiğiniz hello kritik toocreating başarılı bir bağlantı ayarlardır. VPN Gateway’e ilişkin kaynaklar ve ayarlar hakkında bilgi için bkz. [VPN Gateway ayarları hakkında](vpn-gateway-about-vpn-gateway-settings.md). Merhaba makale, ağ geçidi türleri, VPN türleri, bağlantı türleri, ağ geçidi alt ağları, yerel ağ geçitleri ve tooconsider isteyebilirsiniz diğer çeşitli kaynak ayarları anlamak bilgi toohelp içerir.

### <a name="tools"></a>Dağıtım araçları

Oluşturma ve Azure portal hello gibi bir yapılandırma aracını kullanarak kaynakları yapılandırma başlatabilirsiniz. Daha sonra tooconfigure ek kaynaklar, PowerShell gibi tooswitch tooanother aracı karar veya var olan kaynakların uygulanabilir olduğunda değiştirin. Şu anda, her kaynak ve kaynak ayarını hello Azure portal yapılandıramazsınız. Belirli yapılandırma aracı gerektiğinde Merhaba makaleler için her bağlantı topolojisi hello yönergeleri belirtin. 

### <a name="models"></a>Dağıtım modeli

Bir VPN ağ geçidi yapılandırdığınızda, başlangıç adımları atmanız sanal ağınız toocreate kullanılan hello dağıtım modeline bağlı. Örneğin, VNet oluşturduysanız hello Klasik dağıtım modeli kullanılarak hello kılavuzları kullanın ve hello Klasik dağıtımı için yönergeler toocreate model ve VPN ağ geçidi ayarlarını yapılandırın. Dağıtım modelleri hakkında daha fazla bilgi için bkz. [Resource Manager’ı ve klasik dağıtım modellerini anlama](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="diagrams"></a>Bağlantı topolojisi diyagramları

Bu önemli tooknow farklı yapılandırmaları VPN ağ geçidi bağlantıları için kullanılabilir olduğunu gösterir. Gereksinimlerinize en iyi yapılandırma toodetermine gerekir. Merhaba aşağıdaki bölümlerde, VPN ağ geçidi bağlantıları aşağıdaki hello hakkında bilgi ve topoloji diyagramları görüntüleyebilirsiniz: bölümleri aşağıdaki hello listesinde tabloları içerir:

* Kullanılabilir dağıtım modeli
* Kullanılabilir yapılandırma araçları
* Doğrudan tooan makale varsa götüren bağlantılar

Kullanım hello diyagramları ve açıklamaları toohelp gereksinimlerinizi hello bağlantı topolojisi toomatch seçin. Merhaba diyagramları hello başlıca temel topolojileri gösterir, ancak bunu olası toobuild hello diyagramları kılavuz olarak kullanarak daha karmaşık yapılandırmalar.

## <a name="s2smulti"></a>Siteden Siteye ve Çok Siteli (IPsec/IKE VPN tüneli)

### <a name="S2S"></a>Siteden Siteye

Siteden Siteye (S2S) VPN ağ geçidi bağlantısı, IPSec/IKE (IKEv1 veya IKEv2) VPN tüneli üzerinden kurulan bir bağlantıdır. Bir VPN cihazı bulunan bir ortak IP adresi atanmış tooit ve bir NAT'ın arkasında yer almıyor şirket içi S2S bağlantısı gerektirir S2S bağlantıları, şirket içi ve dışı yapılandırmalar ile birlikte karma yapılandırmalar için kullanılabilir.   

![Azure VPN Gateway Siteden Siteye bağlantı örneği](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Çok Siteli

Bu türden bağlantı siteden siteye bağlantı hello çeşididir. Genellikle toomultiple bağlanma şirket içi sitelere birden fazla VPN bağlantısı, sanal ağ geçidinden oluşturun. Birden fazla bağlantıyla çalışırken Yol Tabanlı VPN türü (klasik sanal ağlar ile çalışırken “dinamik ağ geçidi” adıyla kullanılır) kullanmanız gerekir. Her bir sanal ağı yalnızca bir VPN ağ geçidi olabilir çünkü hello ağ geçidi üzerinden tüm bağlantıları hello kullanılabilir bant genişliğini paylaşır. Bu tür genellikle "çok siteli" bağlantı olarak adlandırılır.

![Azure VPN Gateway Çok Siteli bağlantı örneği](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Siteden Siteye ve Çok Siteli için dağıtım modelleri ve yöntemleri

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Noktadan Siteye (SSTP üzerinden VPN)

Bir noktadan siteye (P2S) VPN ağ geçidi tek bir istemci bilgisayardan güvenli bağlantı tooyour sanal ağ oluşturmanıza olanak sağlar. Noktadan siteye VPN bağlantıları tooconnect tooyour VNet uzak bir konumdan, örneğin, evden veya bir Konferanstan telecommuting zaman istediğinizde faydalıdır. Tooconnect tooa VNet gereken yalnızca birkaç istemciniz P2S VPN de yararlı çözüm toouse bir siteden siteye VPN yerine durumdur. 

S2S bağlantılarının aksine, P2S bağlantıları için şirket içi genel kullanıma yönelik IP adresi veya VPN cihazı gerekmez. P2S bağlantılarının S2S bağlantıları kullanılabilir hem bağlantılarını uyumlu için tüm yapılandırma gereksinimleri hello sürece aynı VPN ağ geçidi, hello.

P2S kullanır, Güvenli Yuva Tünel Protokolü (bir SSL tabanlı VPN protokolü, SSTP), hello. P2S VPN bağlantısı, hello istemci bilgisayardan başlatılmasıyla oluşturulur.

![Azure VPN Gateway Noktadan Siteye bağlantı örneği](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>Noktadan Siteye dağıtım modelleri ve yöntemleri

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>Sanal Ağdan Sanal Ağa bağlantılar (IPsec/IKE VPN tüneli)

Sanal ağ tooanother sanal ağ (VNet-VNet) bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil. Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın. Hatta Sanal Ağdan Sanal Ağa iletişimini çok siteli bağlantı yapılandırmalarıyla bile birleştirebilirsiniz. Bu özellik şirket içi ve şirket dışı bağlantıyla ağ içi bağlantıyı birleştiren ağ topolojileri kurabilmenize olanak sağlar.

Bağlandığınız sanal ağlar Hello olabilir:

* Merhaba, aynı ya da farklı bölgelerde
* Merhaba, aynı ya da farklı Aboneliklerde 
* Merhaba, aynı veya farklı dağıtım modeli

![Azure VPN ağ geçidi VNet tooVNet bağlantısı örneği](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>Dağıtım modelleri arasındaki bağlantılar

Azure'ın şu anda iki dağıtım modeli vardır: Klasik ve Resource Manager. Azure'ı bir süredir kullanıyorsanız klasik VNet'te çalışan Azure VM'leriniz ve örnek rollerinizin olması olasıdır. Daha yeni VM'leriniz ve rol örnekleriniz Resource Manager'da oluşturulan bir VNet'te çalışıyor olabilir. Doğrudan kaynaklarla başka bir VNet toocommunicate hello kaynakları hello sanal ağlar tooallow arasında bir bağlantı oluşturabilirsiniz.

### <a name="vnet-peering"></a>VNet eşlemesi

Sanal ağınızı belirli gereksinimleri karşılayan sürece mümkün toouse sanal ağ bağlantınıza, toocreate eşleme olabilir. VNet eşlemesi sanal ağ geçidini kullanmaz. Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Sanal Ağdan Sanal Ağa dağıtım modelleri ve yöntemleri

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (adanmış özel bağlantı)

Microsoft Azure ExpressRoute bağlantı sağlayıcı tarafından kolaylaştırılan adanmış özel bağlantı üzerinden şirket içi ağlarınızı Microsoft bulut hello genişletmenizi sağlar. ExpressRoute ile Microsoft Azure, Office 365 ve CRM Online gibi bağlantıları tooMicrosoft bulut Hizmetleri kurabilirsiniz. Ortak yerleşim tesisinde bağlantı sağlayıcısı üzerinden herhangi bir ağdan herhangi bir ağa (IP VP), noktadan noktaya Ethernet ağı veya sanal çapraz bağlantısından bağlantı olabilir. 

ExpressRoute bağlantıları hello Git değil genel Internet. Bu ExpressRoute bağlantıları toooffer daha fazla güvenilirlik, yüksek hız, düşük gecikme ve normal bağlantıları daha yüksek güvenlik hello Internet sağlar.

ExpressRoute bağlantısı bir VPN ağ geçidi kullanmaz, ancak zorunlu yapılandırmasının bir parçası olarak sanal ağ geçidi kullanır. Bir ExpressRoute bağlantı hello sanal ağ geçidi 'Vpn' yerine 'ExpressRoute' hello ağ geçidi türü ile yapılandırılır. ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute teknik genel bakış](../expressroute/expressroute-introduction.md).

## <a name="coexisting"></a>Siteden Siteye ve ExpressRoute eşzamanlı bağlantıları

ExpressRoute değil WAN bağlantınızdan doğrudan, ayrılmış bir bağlantı (üzerinden değil genel Internet hello) tooMicrosoft Azure gibi hizmetler. Siteden siteye VPN hello şifrelenmiş olarak hareket eder trafiği genel Internet. Merhaba aynı sanal ağ gibi çeşitli avantajları vardır için siteden siteye VPN ve ExpressRoute bağlantılarını mümkün tooconfigure bırakılıyor.

ExpressRoute için güvenli bir yük devretme yolu olarak siteden siteye VPN yapılandırmak veya ağınızın parçası değildir, ancak ExpressRoute aracılığıyla bağlanan siteden siteye VPN tooconnect toosites kullanın. Bu yapılandırma gerektirir iki sanal ağ geçitleri için aynı sanal ağ Merhaba, kullanarak ağ geçidi türü 'Vpn' hello ve diğer 'ExpressRoute' hello ağ geçidi türü kullanılarak hello dikkat edin.

![ExpressRoute ve VPN Gateway eşzamanlı bağlantı örneği](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>S2S ve ExpressRoute dağıtım modelleri ve yöntemleri

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Fiyatlandırma

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

VPN Gateway’e yönelik ağ geçidi SKU’ları hakkında bilgi için bkz. [Ağ geçidi SKU’ları](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="faq"></a>SSS

VPN gateway hakkında sık sorulan sorular için bkz: Merhaba [VPN Gateway SSS](vpn-gateway-vpn-faq.md).

## <a name="next-steps"></a>Sonraki adımlar

- VPN ağ geçidi yapılandırmanızı planlayın. Bkz. [VPN Gateway için Planlama ve Tasarım](vpn-gateway-plan-design.md).
- Görünüm hello [VPN Gateway SSS](vpn-gateway-vpn-faq.md) ek bilgi için.
- Görünüm hello [aboneliği ve hizmet sınırları](../azure-subscription-service-limits.md#networking-limits).
- Merhaba bazıları hakkında bilgi edinin başka bir anahtar [ağı yetenekleri](../networking/networking-overview.md) Azure.
