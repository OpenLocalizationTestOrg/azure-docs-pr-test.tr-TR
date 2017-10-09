---
title: "aaaAzure VPN ağ geçidi SSS | Microsoft Docs"
description: "Merhaba VPN ağ geçidi SSS. Microsoft Azure Sanal Ağ şirket içi ve dışı bağlantılar, karma yapılandırma bağlantıları ve VPN Ağ Geçitleri hakkında SSS."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>VPN Gateway SSS

## <a name="connecting"></a>Toovirtual ağları bağlama

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>Farklı Azure bölgelerinde sanal ağlara bağlanabilir miyim?

Evet. Aslında, hiçbir bölge kısıtlaması yoktur. Bir sanal ağ hello tooanother sanal ağa bağlanabilir aynı bölgede veya farklı bir Azure bölgesi. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>Farklı aboneliklerle sanal ağlara bağlanabilir miyim?

Evet.

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>Tek bir sanal ağdan toomultiple siteleri bağlanabilir miyim?

Windows PowerShell ve hello Azure REST API'lerini kullanarak toomultiple sitelere bağlanabilir. Merhaba bkz [çok siteli ve VNet-VNet bağlantısı](#V2VMulti) SSS bölümüne bakın.

### <a name="what-are-my-cross-premises-connection-options"></a>Şirket içi ve dışı bağlantı seçeneklerim nelerdir?

Aşağıdaki hello bağlantıları desteklenen şirketler arası:

* Siteden Siteye – IPsec üzerinden (IKE v1 ve IKE v2) VPN bağlantısı. Bu bağlantı türüne şirket içi bir VPN cihazı ya da RRAS gerekir. Daha fazla bilgi için bkz. [Siteden Siteye](vpn-gateway-howto-site-to-site-resource-manager-portal.md).
* Noktadan Siteye – SSTP (Güvenli Yuva Tünel Protokolü) üzerinden VPN bağlantısı. Bu bağlantıya VPN cihazı gerekmez. Daha fazla bilgi için bkz. [Noktadan Siteye](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* VNet-VNet – bu türden bağlantı olduğu hello bir siteden siteye yapılandırması ile aynı. VNet tooVNet IPSec üzerinden (IKE v1 ve IKE v2) bir VPN bağlantısıdır. VPN cihazı gerekmez. Daha fazla bilgi için bkz. [Sanal Ağdan Sanal Ağa](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).
* Çok siteli – budur tooconnect sağlayan bir siteden siteye yapılandırmanın bir çeşididir birden çok şirket içi siteler tooa sanal ağ. Daha fazla bilgi için bkz. [Çok Siteli](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).
* ExpressRoute – ExpressRoute değil WAN bağlantınızdan, olmayan bir VPN bağlantısı hello üzerinden doğrudan bağlantı tooAzure genel Internet. Daha fazla bilgi için bkz: Merhaba [ExpressRoute teknik genel bakış](../expressroute/expressroute-introduction.md) ve hello [ExpressRoute SSS](../expressroute/expressroute-faqs.md).

VPN ağ geçidi bağlantıları hakkında daha fazla bilgi için bkz. [VPN Gateway Hakkında](vpn-gateway-about-vpngateways.md).

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>Merhaba bir siteden siteye bağlantı ve noktadan siteye arasındaki fark nedir?

**Siteden Siteye** (IPsec/IKE VPN tüneli) yapılandırmalar, şirket içi konumunuz ile Azure arasında yapılır. Bu, herhangi bir şirket içi tooany sanal makine veya rol örneği tooconfigure Yönlendirme ve izinleri nasıl seçtiğinize bağlı olarak, sanal ağ içinde bulunan bilgisayarlarınızı bağlanabileceği anlamına gelir. Her zaman kullanıma uygun şirket içi ve dışı bağlantı için müthiş bir seçenek; karma yapılandırmalar için de çok uygundur. Bu bağlantı türü, ağınızın hello sınırında dağıtılmalıdır IPSec VPN uygulamasına (donanım veya yazılım aracı) kullanır. toocreate bu tür bir bağlantı NAT'ın arkasında yer almayan dışarıya dönük IPv4 adresi olmalıdır

**Noktası Site** (VPN üzerinden SSTP) yapılandırmaları tooanything sanal ağınızda bulunan her yerden tek bir bilgisayardan bağlanmanızı sağlar. Merhaba Windows yerleşik VPN istemcisi kullanır. Merhaba noktadan siteye yapılandırmasının bir parçası olarak, bir sertifika ve bilgisayar tooconnect tooany sanal makine veya rol örneği hello sanal ağ içinde izin hello ayarlarını içeren bir VPN istemcisi yapılandırma paketini yükleyin. Tooconnect tooa sanal ağ istiyor, ancak şirket içinde olmayan çok yararlıdır. Erişim tooVPN donanım ya da her ikisi de siteden siteye bağlantı için gerekli olan bir dışarıya dönük IPv4 adresi olmadığında da iyi bir seçenek değil.

Noktası siteye eşzamanlı olarak, bir rota tabanlı VPN kullanarak siteden siteye bağlantınızı oluşturmak sürece, ağ geçidiniz için yazın ve her iki Site siteye, sanal ağ toouse yapılandırabilirsiniz. Rota tabanlı VPN türlerine hello Klasik dağıtım modelinde dinamik ağ geçitleri adı verilir.

## <a name="gateways"></a>Sanal ağ geçitleri

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>VPN ağ geçidi bir sanal ağ geçidi midir?

VPN ağ geçidi bir sanal ağ geçidi türüdür. VPN ağ geçidi, şifrelenmiş trafiği bir genel bağlantı üzerinden sanal ağınız ile şirket içi konumunuz arasında gönderir. Sanal ağlar arasında bir VPN ağ geçidi toosend trafiği de kullanabilirsiniz. Bir VPN ağ geçidi oluşturduğunuzda, hello - GatewayType değeri 'Vpn' kullanın. Daha fazla bilgi için bkz. [VPN Gateway yapılandırma ayarları hakkında](vpn-gateway-about-vpn-gateway-settings.md).

### <a name="what-is-a-policy-based-static-routing-gateway"></a>İlke tabanlı (statik yönlendirme) ağ geçidi nedir?

İlke tabanlı ağ geçitleri, ilke tabanlı VPN'leri uygular. İlke temelli VPN'ler, şifrelemek ve hello şirket içi ağınız ve hello Azure Vnet'iniz arasında adres öneklerinin birleşimleri temelindeki IPSec tüneller üzerinden paketleri doğrudan. Merhaba ilke (veya trafik Seçici) çoğunlukla hello VPN yapılandırmasında bir erişim listesi olarak tanımlanır.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>Rota tabanlı (dinamik yönlendirme) ağ geçidi nedir?

Rota tabanlı ağ geçitleri uygulama yol tabanlı VPN'leri hello. Rota temelli VPN'ler, iletme veya yönlendirme tablosu toodirect paketleri kendi ilgili arabirimlerine yönlendirmek hello IP "yolları" kullanın. Tünel arabirimleri hello sonra karşılama paketleri hello tüneller ve şifresini çözmek veya şifreleme. Rota temelli VPN'ler olarak any herhangi yapılandırılmış için ilke veya trafik Seçici Hello (veya joker karakterler).

### <a name="do-i-need-a-gatewaysubnet"></a>'GatewaySubnet' gerekli mi?

Evet. Merhaba ağ geçidi alt ağı hello sanal ağ geçidi hizmetlerini kullanma hello IP adreslerini içerir. Sipariş tooconfigure bir sanal ağ geçidi, sanal ağınızda için toocreate bir ağ geçidi alt ağı gerekir. Tüm ağ geçidi alt ağları 'GatewaySubnet' toowork düzgün olarak adlandırılmalıdır. Ağ geçidi alt ağını başka şekilde adlandırmayın. Ve Vm'leri veya herhangi bir şey başka toohello ağ geçidi alt ağı dağıtmazsınız.

Merhaba ağ geçidi alt ağı oluşturduğunuzda, alt ağ hello IP adreslerinin sayısı hello içerdiğini belirtin. Merhaba ağ geçidi alt ağı Hello IP adresleri toohello ağ geçidi hizmeti ayrılır. Diğerleri çok daha fazla IP adreslerini toobe toohello ağ geçidi Hizmetleri ayrılan. bazı yapılandırmalar gerektirir. Ağ geçidi alt ağı yeterli IP adreslerini tooaccommodate Gelecekteki büyümeyi ve olası ek yeni bağlantı yapılandırmaları içerdiğinden emin toomake istiyor. Bu nedenle, /29 kadar küçük bir ağ geçidi alt ağı oluşturmanız mümkün olsa da /27 veya daha büyük bir (/27, /26, /25 vb.) ağ geçidi alt ağı oluşturmanız önerilir. Merhaba yapılandırma hello gereksinimleri toocreate istiyorsanız ve elinizde o hello ağ geçidi alt ağı bu gereksinimlerini karşılayacak doğrulayın bakın.

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>Sanal makineleri veya rol örneklerini toomy ağ geçidi alt ağı dağıtabilir miyim?

Hayır.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>Oluşturmadan önce VPN ağ geçidi IP adresimi alabilir miyim?

Hayır. Ağ geçidi ilk tooget hello IP adresiniz toocreate var. Başlangıç IP adresi değişiklikleri silerseniz ve VPN ağ geçidinizi yeniden oluşturun.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>VPN ağ geçidim için bir Statik Genel IP adresi isteğinde bulunabilir miyim?

Hayır. Yalnızca Dinamik IP adresi ataması desteklenir. Ancak, bu tooyour VPN ağ geçidi atandıktan sonra hello IP adresini değiştirse anlamına gelmez. ağ geçidi Hello VPN ağ geçidi IP adresi değişiklikleri hello zaman hello yalnızca zaman silinmiş ve yeniden oluşturulmalıdır. Merhaba VPN ağ geçidi genel IP adresi yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında VPN ağ geçidi değiştirmez. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>VPN tünelimin kimliği nasıl doğrulanır?

Azure VPN PSK (Önceden Paylaşılan Anahtar) kimlik doğrulamasını kullanır. Biz hello VPN tüneli oluşturduğunuzda, biz önceden paylaşılan anahtar (PSK) oluşturur. Merhaba otomatik olarak oluşturulan PSK tooyour hello ayarlamak önceden paylaştırılan anahtar PowerShell cmdlet'ini veya REST API ile kendi değiştirebilirsiniz.

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>Merhaba önceden paylaşılan anahtar API'sini Ayarla tooconfigure ilke tabanlı my kullanabilirim (statik yönlendirme) ağ geçidi VPN?

Merhaba ayarlamak önceden paylaşılan anahtar API'sini ve PowerShell cmdlet'ini kullanılan tooconfigure Evet, olabilir hem Azure ilke tabanlı (statik) VPN'ler hem de rota tabanlı (dinamik) yönlendirme VPN'leri.

### <a name="can-i-use-other-authentication-options"></a>Diğer kimlik doğrulama seçeneklerini kullanabilir miyim?

Sınırlı toousing önceden paylaşılan anahtarı (PSK) kimlik doğrulaması için duyuyoruz.

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>Ne t belirtin, trafiği hello VPN ağ geçidi üzerinden gider mi?

#### <a name="resource-manager-deployment-model"></a>Resource Manager dağıtım modeli

* PowerShell: "AddressPrefix" toospecify trafiği hello yerel ağ geçidi için kullanır.
* Azure portal: toohello yerel ağ geçidi gidin > yapılandırma > adres alanı.

#### <a name="classic-deployment-model"></a>Klasik dağıtım modeli

* Azure portal: toohello Klasik sanal ağ gidin > VPN bağlantıları > siteden siteye VPN bağlantıları > yerel site adı > yerel site > istemci adres alanı. 
* Klasik portal: hello ağlar sayfasında yerel ağlar altında sanal ağınız için hello ağ geçidi üzerinden gönderilen istediğiniz aralığı ekleyin. 

### <a name="can-i-configure-forced-tunneling"></a>Zorlamalı Tüneli yapılandırabilir miyim?

Evet. Bkz. [Zorlamalı tüneli yapılandırma](vpn-gateway-about-forced-tunneling.md).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>I kendi VPN sunucumu Azure ayarlayabilir ve tooconnect toomy şirket içi ağı kullanmak?

Evet, kendi VPN ağ geçitleri veya sunucularınızı ister Azure Marketi hello veya kendi VPN yönlendiricilerinizi oluşturarak dağıtabilirsiniz. Tooconfigure kullanıcı tanımlı yollar gereksinim, sanal ağınızda bulunan, şirket içi ağlarınız ve sanal ağ alt ağları arasında düzgün tooensure trafik yönlendirilir.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>Neden belirli bağlantı noktaları VPN ağ geçidimde açık?

Azure altyapı iletişimi için gereklidirler. Bunlar Azure sertifikaları tarafından korunur (kilitlenir). Uygun sertifikaları olmadan, bu ağ geçitlerinin müşterileri hello dahil dış varlıklar, bu bitiş noktasında herhangi bir efekt mümkün toocause olmaz.

Bir VPN ağ geçidi temelde çok konaklı hello müşteri özel ağ ve bir NIC karşılıklı hello ortak ağ dokunarak bir NIC ile aygıttır. Altyapı iletişimi için ihtiyaç duydukları tooutilize ortak uç noktaları için azure altyapı varlıkları uyum nedenleriyle müşterinin özel ağlarına dokunun olamaz. Merhaba ortak uç noktalar düzenli aralıklarla Azure güvenlik denetimi tarafından taranır.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Ağ geçidi türleri, gereksinimleri ve verimliliği hakkında daha fazla bilgi

Daha fazla bilgi için bkz. [VPN Gateway yapılandırma ayarları hakkında](vpn-gateway-about-vpn-gateway-settings.md).

## <a name="s2s"></a>Siteden Siteye bağlantılar ve VPN cihazları

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>VPN cihazını seçerken nelere dikkat etmeliyim?

Cihaz satıcılarıyla işbirliğiyle bir dizi standart Siteden Siteye VPN cihazını doğruladık. Bilinen uyumlu VPN cihazları, ilgili yapılandırma yönergeleri veya örnekleri ve cihaz özellikleri listesi hello bulunabilir [VPN cihazları hakkında](vpn-gateway-about-vpn-devices.md) makalesi. Bilinen uyumlu olarak listelenen hello cihaz ailelerindeki tüm cihazlar, sanal ağ ile çalışması gerekir. toohelp VPN Cihazınızı yapılandırmak, toohello cihazı yapılandırma örneğini veya tooappropriate cihaz ailesine karşılık gelen bağlantıya bakın.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>VPN cihazı yapılandırma ayarlarını nerede bulabilirim?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>VPN cihazı yapılandırma örneklerini nasıl düzenleyebilirim?

Cihaz yapılandırma örneklerini düzenleme hakkında daha fazla bilgi için bkz. [Örnekleri düzenleme](vpn-gateway-about-vpn-devices.md#editing).

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>IPsec ve IKE parametrelerini nerede bulabilirim?

IPsec/IKE parametreleri için bkz. [Parametreler](vpn-gateway-about-vpn-devices.md#ipsec).

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>Trafik boştayken neden ilke tabanlı VPN tünelim kayboluyor?

İlke tabanlı (statik rota olarak da bilinir) VPN Ağ geçitleri için bu beklenen bir davranıştır. 5 dakikadan fazla hello tüneli üzerinden Hello trafik boştayken hello tünel bozulur. Herhangi bir yönde akan trafik başladığında, hello tünel hemen yeniden.

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>Yazılım VPN tooconnect tooAzure kullanabilir miyim?

Siteden Siteyi şirket içi ve dışı yapılandırması için Windows Server 2012 Yönlendirme ve Uzaktan Erişim (RRAS) sunucularını destekliyoruz.

Tooindustry standardı IPSec uygulamalarıyla uyumlu olduğu sürece diğer yazılım VPN çözümleri bizim ağ geçidimizle çalışmalıdır. Yapılandırma ve destek hakkında yönergeler için hello yazılım Hello satıcısına başvurun.

## <a name="P2S"></a>Noktadan Siteye bağlantıları

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>Sanal Ağdan Sanal Ağa ve Çok Siteli bağlantılar

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>Azure VPN ağ geçidi tootransit trafiği kendi şirket içi siteler veya tooanother sanal ağ arasında kullanabilir miyim?

**Resource Manager dağıtım modeli**<br>
Evet. Merhaba bkz [BGP](#bgp) daha fazla bilgi için bölüm.

**Klasik dağıtım modeli**<br>
Azure VPN ağ geçidi üzerinden trafik hello Klasik dağıtım modeli kullanılarak mümkündür, ancak hello ağ yapılandırma dosyasında istatistiksel olarak tanımlanan adres alanları kullanır. BGP hello Klasik dağıtım modelini kullanarak Azure sanal ağlar ve VPN ağ geçitleri ile henüz desteklenmiyor. BGP olmadan, geçiş adres alanlarının el ile tanımlanması çok hata eğilimindedir ve önerilmez.

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>Azure aynı IPSec/IKE önceden paylaşılan hello üretin tüm VPN bağlantılarımla hello için aynı anahtar sanal ağ?

Hayır, varsayılan olarak Azure farklı VPN bağlantıları için farklı önceden paylaşılan anahtarlar oluşturur. Ancak, tercih ettiğiniz hello ayarlamak VPN ağ geçidi anahtarı REST API veya PowerShell cmdlet tooset hello anahtar değerini kullanabilirsiniz. Merhaba anahtar uzunluğu 1 too128 karakter arasında alfasayısal bir dize olmalıdır.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>Daha fazla Siteden Siteye VPN ile tek bir sanal ağa göre daha fazla bant genişliği elde edebilir miyim?

Hayır, noktadan siteye VPN'lerde dahil tüm VPN tünelleri aynı Azure VPN ağ geçidi ve hello kullanılabilir bant genişliğini hello.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>Çok siteli VPN kullanarak sanal ağlarım ve şirket içi sitem arasında birden fazla tünel yapılandırabilir miyim?

Evet, ancak her iki tüneller toohello BGP yapılandırmalısınız aynı konumu.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>Birden çok VPN tüneline sahip sanal ağımla birlikte Noktadan Siteye VPN’lerini kullanabilir miyim?

Evet, noktadan siteye (P2S) VPN'ler toomultiple şirket içi sitelere ve başka sanal ağlara bağlanma hello VPN ağ geçitleri ile kullanılabilir.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>Bir sanal ağ IPSec VPN toomy expressroute bağlantı hattı bağlanabilir miyim?

Evet, bu desteklenir. Daha fazla bilgi için bkz. [Bir arada var olan ExpressRoute ve Siteden Siteye VPN bağlantıları yapılandırma](../expressroute/expressroute-howto-coexist-classic.md).

## <a name="ipsecike"></a>IPsec/IKE ilkesi

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>Şirket içi ve dışı bağlantısı ve VM'ler

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>Sanal Makinem sanal bir ağa ise ve bir şirket içi bağlantınız nasıl toohello VM bağlanacağını?

Birkaç seçeneğiniz vardır. VM için etkin RDP varsa, hello özel IP adresini kullanarak tooyour sanal makineye bağlanabilir. Bu durumda, hello özel IP adresi ve başlangıç bağlantı noktası tooconnect çok (genellikle 3389) istediğinizi belirtmeniz gerekir. Merhaba trafiği için sanal makinenizde tooconfigure hello bağlantı noktası gerekir.

Başka bir sanal makineden hello üzerinde aynı bulunan özel IP adresiyle tooyour sanal makineye bağlanabildiğinizi sanal ağ. Sanal ağınızın dışında bir konumdan bağlanıyorsanız hello özel IP adresini kullanarak RDP tooyour sanal makineye uygulanamaz. Örneğin, yapılandırılmış bir noktadan siteye sanal ağınız varsa ve bilgisayarınızdan bağlantı kurmak olmayan özel IP adresine göre toohello sanal makineye bağlanamıyor.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>Sanal Makinem şirket içi bağlantılar sahip bir sanal ağ içinde ise, VM'me ait tüm hello trafiğin Bu bağlantı üzerinden gider?

Hayır. Bir hedefe sahip hello trafik belirttiğiniz hello sanal ağ yerel ağ IP adresi aralıklarında bulunan IP hello sanal ağ geçidinden geçer. Trafik hello sanal ağda bulunan IP hello sanal ağ içinde kalacak hedefi olur. Diğer trafik hello yük dengeleyici toohello genel ağlar gönderilen veya zorlamalı tünel kullanılırsa, hello Azure VPN ağ geçidi üzerinden gönderilir.

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>RDP bağlantı tooa VM nasıl sorun giderme

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Sanal Ağ SSS

Hello ek sanal ağ bilgilerini [Virtual Network SSS](../virtual-network/virtual-networks-faq.md).

## <a name="next-steps"></a>Sonraki adımlar

* VPN Gateway hakkında daha fazla bilgi için bkz. [VPN Gateway Hakkında](vpn-gateway-about-vpngateways.md).
* VPN Gateway yapılandırma ayarları hakkında daha fazla bilgi için bkz. [VPN Gateway yapılandırma ayarları hakkında](vpn-gateway-about-vpn-gateway-settings.md).
