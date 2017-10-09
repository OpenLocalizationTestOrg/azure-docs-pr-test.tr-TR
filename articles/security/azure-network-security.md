---
title: "aaaAzure ağ güvenliği | Microsoft Docs"
description: "Geniş işlem örnekleri dahil bulut tabanlı bilgi işlem Hizmetleri & otomatik olarak toomeet hello ihtiyaçlarını uygulamanızı veya Kurumsal yukarı ve aşağı ölçeklenebilen hizmetleri hakkında bilgi edinin."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Azure ağ güvenliği

Güvenlik hello bulutta iş ve nasıl önemli Azure güvenliği hakkında doğru ve güncel bilgi bulma olduğunu olduğunu biliyoruz. Merhaba en iyi uygulamalar ve hizmetler için nedenleri toouse Azure Azure'nın çeşitli güvenlik araçları ve yetenekleri tootake avantajlarından biri. Bu araçları ve yetenekleri hello Azure platformu üzerinde olası toocreate güvenli çözümleri olun yardımcı olur.

Microsoft Azure gizlilik, bütünlük ve müşteri verilerini, kullanılabilirliğini de saydam sorumluluk etkinleştirirken sağlar. toohelp, daha iyi anlamak hello Müşteri'nin açısından Microsoft Azure içinde uygulanan ağ güvenlik denetimleri hello koleksiyonu, bu makalede, "Azure ağ güvenliği" tooprovide yazılır hello ağ güvenliği kapsamlı bakma denetimleri Microsoft Azure ile kullanılabilir.

Bu yazı, ağ hello çeşitli hakkında denetimleri tooinform Azure'da tooenhance hello güvenliği dağıttığınız hello çözümlerinin yapılandırabilirsiniz yöneliktir. İlgileniyorsanız hangi Microsoft Azure platformu kendisini toosecure hello ağ dokusu Merhaba, hello hello Azure güvenlik bölümüne bakın [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/azure-security).

## <a name="azure-platform"></a>Azure platformu

Azure işletim sistemleri, programlama dilleri, çerçeveleri, Araçlar, veritabanları ve aygıtları geniş çapta destekleyen bir genel bulut hizmeti platformudur.  Docker Tümleştirmesi ile Linux kapsayıcıları çalıştırabilirsiniz; JavaScript, Python, .NET, PHP, Java ve Node.js ile uygulamalar oluşturma; Yapı geri-iOS, Android ve Windows cihazları sona erer. Azure bulut hizmetlerine geliştiriciler ve BT uzmanları, aynı teknolojileri milyonlarca zaten kullanır ve güven hello destekler.

Oluşturmanıza veya BT varlıklar bir genel bulut hizmeti sağlayıcısına geçiş yapma, uygulamalarınızı, bir kuruluşun yeteneklerini tooprotect üzerinde bağlı ve hizmetler ve hello denetimleri ile veri hello olduğunda, bulut tabanlı toomanage hello güvenliğini sağlarlar. varlıklar.

Azure'un altyapısından aynı anda milyonlarca müşteri barındırmak için hello tesis tooapplications gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar. Ayrıca, Azure, kapsamlı bir yapılandırılabilir güvenlik seçenekleri ve hello özelliği toocontrol koleksiyonuyla sağlar bunları böylece güvenlik toomeet hello benzersiz gereksinimleri, kuruluşunuzun dağıtımlarının özelleştirebilirsiniz.

## <a name="abstract"></a>Özet

Microsoft Genel bulut Hizmetleri hiper ölçekli hizmetler ve altyapı, Kurumsal düzeydeki özellikleri ve karma bağlantı için birçok seçenek sunar. Bu hizmetler hello Internet üzerinden veya özel ağ bağlantısı sağlayan Azure ExpressRoute ile tooaccess seçebilirsiniz. Merhaba Microsoft Azure platformu sağlar, tooseamlessly hello bulutunu altyapınızı genişletme ve çok katmanlı mimarileri oluşturun. Ayrıca, üçüncü tarafların güvenlik hizmetleri ve sanal gereçler sunarak Gelişmiş özellikleri etkinleştirebilirsiniz.

Azure Ağ Hizmetleri tasarım gereği esneklik, kullanılabilirlik, dayanıklılık, güvenlik ve bütünlüğü ekranı kaplamasını sağlayın. Bu teknik incelemede Azure ağ işlevlerini hello ayrıntıları ve müşterilerin Azure'nın yerel güvenlik özellikleri toohelp nasıl kullanabileceğiniz hakkında bilgi kendi bilgi varlıklarını koruma sağlar.

Bu teknik kitleleri içeren Hello verilmektedir:

- Teknik yöneticileri, ağ yöneticileri ve güvenlik çözümleri kullanılabilir ve desteklenen Azure arıyorsunuz geliştiriciler.

-   SME veya tooget üst düzey bir genel bakış istediğiniz iş işlemi Yöneticiler Azure ağ teknolojileri ve ağ güvenliği hello Azure genel bulut tartışmalarını ilgili hizmetleri hello.

## <a name="azure-networking-big-picture"></a>Büyük resim ağ azure
Microsoft Azure, uygulama ve hizmet bağlantı gereksinimleri sağlam bir ağ altyapısı toosupport içerir. Azure'da, şirket içi arasında bulunan kaynaklar arasındaki ağ bağlantısı mümkündür ve Azure kaynakları ve hello Internet gelen tooand ve Azure barındırılır.

![Büyük resim ağ azure](media/azure-network-security/azure-network-security-fig-1.png)

Merhaba [Azure ağ altyapısı](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) , toosecurely bağlanmak tooeach Azure kaynaklarını diğer sanal ağlar (Vnet'ler) etkinleştirir. Bir VNet kendi ağ hello bulutta gösterimidir. VNet mantıksal ayırma hello Azure bulut ayrılmış ağ tooyour aboneliğin ' dir. Sanal ağlar tooyour şirket içi ağlara bağlanabilir.

Azure destekler, WAN bağlantısının bağlantı tooyour şirket içi ağ ve bir Azure sanal ağı ile ayrılmış [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Azure ile siteniz arasında Hello bağlantısını kullanan hello geçmez adanmış bir bağlantı genel Internet. Azure uygulamanız birden çok veri merkezlerinde çalıştığından, kullanabileceğiniz [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) kullanıcıların akıllıca hello uygulama örnekleri arasında tooroute isteklerini. Ayrıca Internet hello erişilebilir olup olmadığını Azure üzerinde çalışmayan trafiği tooservices yönlendirebilirsiniz.

## <a name="enterprise-view-of-azure-networking-components"></a>Azure ağ bileşenlerinin Kurumsal görünümü
Azure ilgili toonetwork güvenlik tartışmaları birçok ağ bileşenleri içerir. Biz bu ağ bileşenlerini açıklar ve hello güvenlik odaklanan ilgili toothem verir.

> [!Note]
> Azure ağı tüm yönlerini açıklanan – yalnızca toobe bileşendirler planlama ve Azure'da dağıtımı uygulamaları ve Hizmetleri geçici güvenli ağ altyapısını tasarlama kabul aşağıdakiler ele.

Bu yazıda, kapak hello Azure ağı Kurumsal yetenekleri şu:

-   Temel ağ bağlantısı

-   Karma bağlantı

-   Güvenlik denetimleri

-   Ağ doğrulama

### <a name="basic-network-connectivity"></a>Temel ağ bağlantısı

Merhaba [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) , toosecurely bağlanmak tooeach Azure kaynaklarını diğer sanal ağ (VNet) hizmetini sağlar. Bir VNet kendi ağ hello bulutta gösterimidir. VNet mantıksal ayırma hello Azure ağ altyapısı ayrılmış tooyour aboneliğin ' dir. Diğer sanal ağlar tooeach da bağlanabilirsiniz ve tooyour şirket içi siteden siteye VPN kullanarak ağları ve ayrılmış [WAN bağlantıları](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

![Temel ağ bağlantısı](media/azure-network-security/azure-network-security-fig-2.png)

Azure'da Vm'leri toohost sunucuları kullandığının anlaşılması hello ile bu VM'lerin tooa ağ nasıl bağlanacağını hello soru olur. Merhaba VM'ler tooan bağlanmak cevaptır [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

Azure sanal ağları olan hello sanal ağlar gibi şirket içi Microsoft Hyper-V veya VMware gibi kendi sanallaştırma platformunu çözümleriyle kullanın.

#### <a name="intra-vnet-connectivity"></a>İçi-VNet bağlantısı

Sanal ağlar tooeach diğer bağlanabilir, kaynakları etkinleştirme tooeither VNet toocommunicate birbirleri ile sanal ağlar bağlanır. Veya her ikisini seçenekleri tooconnect sanal ağlar tooeach diğer aşağıdaki hello kullanabilirsiniz:

- **Eşliği:** etkinleştirir kaynaklara bağlı hello içinde toodifferent Azure Vnet birbiriyle aynı Azure konumuna toocommunicate. Merhaba kaynaklara bağlı toohello değilmiş gibi hello bant genişliği ve VNet olduğu hello arasında gecikme süresi aynı hello aynı sanal ağı. eşleme, hakkında daha fazla toolearn okuma [sanal ağ eşlemesi](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

 ![Eşleme](media/azure-network-security/azure-network-security-fig-3.png)

- **VNet-VNet bağlantısı:** etkinleştirir kaynaklara bağlı toodifferent Azure VNet hello içinde aynı veya farklı Azure konumu. Bir Azure VPN ağ geçidi üzerinden trafik akışı gerekir çünkü eşliği farklı olarak, bant genişliği sanal ağlar arasında sınırlıdır.

![VNet-VNet bağlantısı](media/azure-network-security/azure-network-security-fig-4.png)


Merhaba okuma bir VNet-VNet bağlantısı ile sanal ağlara bağlanma hakkında daha fazla toolearn [VNet-VNet bağlantı makale yapılandırma](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="azure-virtual-network-capabilities"></a>Azure sanal ağ özellikleri:

Gördüğünüz gibi bir Azure sanal ağı tooother ağ kaynaklarına güvenli bir şekilde bağlanabilmesi için sanal makineleri tooconnect toohello ağ sağlar. Ancak, temel bağlantıyı yalnızca hello başlangıçtır. Merhaba hello Azure Virtual Network service aşağıdaki özelliklerini hello Azure sanal ağ güvenlik özelliklerini kullanır:

-   Yalıtım

-   İnternet bağlantısı

-   Azure kaynak bağlantısı

-   VNet bağlantısı

-   Şirket içi bağlantı

-   Trafik filtreleme

-   Yönlendirme

**Yalıtım**

Sanal ağlar olan [yalıtılmış](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) birbirinden. Geliştirme, test ve üretim kullanımı aynı hello için ayrı sanal ağlar oluşturabilirsiniz [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) adres blokları. Buna karşılık, ağları birbirine bağlamak ve farklı CIDR adres bloklarını kullanan birden çok sanal ağlar oluşturabilirsiniz. Bir sanal ağ birden çok alt ağa bölebilirsiniz.

Azure VM'ler için dahili ad çözümlemesi sağlar ve [bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services/) rol örnekleri tooa VNet bağlı. Bu gibi durumlarda, bir VNet toouse isteğe bağlı olarak Azure dahili ad çözümlemesi yerine kendi DNS sunucularınızı yapılandırabilirsiniz.

Her Azure içinde birden çok sanal ağlar uygulayabilirsiniz [abonelik](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) ve Azure [bölge](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json). Her sanal ağ, diğer sanal ağlardan yalıtılır. Her sanal ağ için şunları yapabilirsiniz:

-   Ortak ve özel (RFC 1918) adreslerini kullanarak özel bir özel IP adres alanını belirtin. Azure kaynakları bağlı toohello VNet özel bir IP adresi hello adres alanından atar, atadığınız.

-   Bir veya daha fazla alt ağ içinde Hello VNet segmentlere ayırmak ve hello sanal adres alanı tooeach alt kısmı paylaştırabilirsiniz.

-   Azure tarafından sağlanan ad çözümlemesi kullanın veya kaynaklar tarafından kullanılmak üzere kendi DNS sunucusu tooa VNet bağlı belirtin. Merhaba okuma vnet'lerdeki ad çözümlemesi hakkında daha fazla toolearn [VM'ler ve bulut Hizmetleri için ad çözümlemesi](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

**İnternet bağlantısı**

Tüm [Azure sanal makineler (VM)](https://docs.microsoft.com/azure/virtual-machines/windows/) ve bulut Hizmetleri rol örnekleri bağlı tooa VNet sahip toohello Internet, varsayılan olarak erişebilirsiniz. Gelen erişim toospecific kaynakları, gerektiğinde de etkinleştirebilirsiniz. (VM) ve bulut Hizmetleri rol örnekleri bağlı tooa VNet sahip toohello Internet, varsayılan olarak erişebilirsiniz. Gelen erişim toospecific kaynakları, gerektiğinde de etkinleştirebilirsiniz.

Tüm kaynaklara bağlı tooa VNet varsayılan giden bağlantı toohello Internet vardır. Merhaba özel IP adresi hello kaynağının kaynak ağ adresi (SNAT) tooa genel IP adresi hello Azure altyapısı tarafından çevrilen değil. Özel Yönlendirme ve trafik filtreleme uygulayarak hello varsayılan bağlantı değiştirebilirsiniz. Merhaba okuma giden Internet bağlantısı hakkında daha fazla toolearn [azure'da giden bağlantılar anlama](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json).

toocommunicate Internet SNAT, bir kaynak olmadan genel bir IP adresi atanmalıdır hello Internet ya da toocommunicate giden toohello tooAzure kaynaklardan gelen. Merhaba okuma genel IP adresleri hakkında daha fazla toolearn [ortak IP adresleri](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address).

**Azure kaynak bağlantısı**

[Azure kaynaklarını](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) gibi bağlı toohello bulut Hizmetleri ve sanal makineleri aynı sanal ağı. Merhaba kaynakları tooeach diğer bağlanabilir özel IP adresleri, farklı alt ağlarda olsalar bile. Azure yoksa tooconfigure ve yollar yönetmek için varsayılan alt ağlar, sanal ağlar ve şirket içi ağlar arasında yönlendirme sağlar.

Birkaç Azure kaynaklarını tooa sanal makineler (VM), bulut Hizmetleri, uygulama hizmeti ortamları ve sanal makine ölçek kümeleri gibi VNet bağlanabilir. VM'ler tooa alt ağ bir sanal ağ içindeki ağ arabirimi (NIC) üzerinden bağlanır. NIC'ler, hello okuma hakkında daha fazla toolearn [ağ arabirimleri](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface).

**VNet bağlantısı**

[Sanal ağlar](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) bağlı tooeach diğer, kaynakları etkinleştirme bağlı tooany VNet toocommunicate başka bir VNet üzerinde herhangi bir kaynağa sahip.

Sanal ağlar tooeach diğer bağlanabilir, kaynakları etkinleştirme tooeither VNet toocommunicate birbirleri ile sanal ağlar bağlanır. Veya her ikisini seçenekleri tooconnect sanal ağlar tooeach diğer aşağıdaki hello kullanabilirsiniz:

- **Eşliği:** etkinleştirir kaynaklara bağlı hello içinde toodifferent Azure Vnet birbiriyle aynı Azure konumuna toocommunicate. Merhaba bant genişliği ve sanal ağlar olduğu hello aynı hello kaynaklara bağlı toohello olsaydı hello arasında gecikme eşliği, hakkında daha fazla aynı VNet.toolearn okuma hello [sanal ağ eşlemesi](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

- **VNet-VNet bağlantısı:** etkinleştirir kaynaklara bağlı toodifferent Azure VNet hello içinde aynı veya farklı Azure konumu. Bir Azure VPN ağ geçidi üzerinden trafik akışı gerekir çünkü eşliği farklı olarak, bant genişliği sanal ağlar arasında sınırlıdır. toolearn VNet-VNet bağlantısı ile sanal ağlara bağlanma hakkında daha fazla. daha fazlasını okuyun hello toolearn [VNet-VNet bağlantı yapılandırma](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) .

**Şirket içi bağlantı**

Sanal ağlar bağlanması çok[şirket içi](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) ağları veya siteden siteye VPN bağlantısı hello Internet üzerinden ağınız ve Azure arasında özel ağ bağlantıları üzerinden.

Şirket içi ağ tooa seçenekleri aşağıdaki hello herhangi bir bileşimini kullanarak VNet bağlanabilir:

- **Noktadan siteye sanal özel ağ (VPN):** bir tek PC bağlı tooyour ağ ile Merhaba VNet arasında kuruldu. Çok az kayıpla veya hiç değişiklik tooyour mevcut ağ gerektirdiğinden bu bağlantı türü, yalnızca Azure ile ya da geliştiricileri için başlıyorsanız mükemmeldir. Merhaba bağlantı hello SSTP Protokolü şifrelenmiş tooprovide iletişimi hello PC ve hello VNet arasında hello Internet üzerinden kullanır. Noktadan siteye VPN için hello gecikme süresini öngörülemeyen olduğu Hello trafiği hello Internet erişir.

- **Siteden siteye VPN:** VPN cihazınız arasındaki bir Azure VPN ağ geçidi kuruldu. Bu bağlantı türü tooaccess VNet yetkilendirmek herhangi bir şirket içi kaynak sağlar. Merhaba, şirket içi cihaz hello Azure VPN ağ geçidi arasındaki hello Internet üzerinden şifrelenmiş iletişimi sağlayan bir IPSec/IKE VPN bağlantısıdır. siteden siteye bağlantı hello gecikme Hello trafiğin hello Internet geçeceğini öngörülemeyen taşımaktadır.

- **Azure ExpressRoute:** ağınız ve Azure arasında bir expressroute bağlantı ortağı ile oluşturulmuş. Bu bağlantı özeldir. Trafik hello Internet erişmez. ExpressRoute bağlantısı için hello gecikme süresini tahmin edilebilir olduğu hello Internet trafiği çapraz geçiş değil. Merhaba okuma tüm hello önceki bağlantı seçenekleri hakkında daha fazla toolearn [bağlantı topoloji diyagramları](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

**Trafik filtreleme**

VM ve bulut Hizmetleri rol örnekleri [ağ trafiğini](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) gelen ve giden kaynak IP adresi ve bağlantı noktası, hedef IP adresi ve bağlantı noktası ve protokol göre filtrelenebilir.

Ağ trafiği veya her ikisini seçenekleri aşağıdaki hello kullanarak alt ağlar arasında filtreleyebilirsiniz:

- **Ağ güvenlik grubu (NSG):** her NSG, kaynak ve hedef IP adresi, bağlantı noktası ve protokol toofilter trafiğini etkinleştiren birden fazla gelen ve giden güvenlik kuralları içerebilir. Bir NSG tooeach bir VM'de NIC uygulayabilirsiniz. Bir NSG toohello alt bir NIC de uygulayabilir veya diğer Azure kaynak bağlı. Merhaba okuma Nsg'ler hakkında daha fazla toolearn [ağ güvenlik grupları](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

- **Sanal ağ uygulamaları:** bir güvenlik duvarı gibi bir ağ işlevi gerçekleştiren yazılımı çalıştıran bir VM sanal ağ Gereci değil. Hello Azure Marketi kullanılabilir NVAs listesini görüntüleyin. NVAs WAN iyileştirmesi ve diğer ağ trafiği işlevleri sağlayan de kullanılabilir durumdadır. NVAs, kullanıcı tanımlı ile genellikle kullanılır ya da BGP yolları. Sanal ağlar arasında bir NVA toofilter trafiği de kullanabilirsiniz.

**Yönlendirme**

İsteğe bağlı olarak, kendi yolları yapılandırmak veya bir ağ geçidi üzerinden BGP yollarını kullanarak yönlendirme Azure'un varsayılan ayarlarını geçersiz kılabilir.

Azure kaynakları bağlı tooany alt ağda birbiriyle, varsayılan olarak tüm VNet toocommunicate etkinleştirmek yönlendirme tabloları oluşturur. Ya da uygulayabilir veya seçenekleri toooverride aşağıdaki hello her ikisi de Azure oluşturduğu varsayılan yolların hello:

- **Kullanıcı tanımlı yollar:** özel yol tablolarını her alt ağ trafiği yönlendirilmiş toofor olduğu denetleyen yollar oluşturabilirsiniz. Merhaba okuyun, kullanıcı tanımlı yollar hakkında daha fazla toolearn [kullanıcı tanımlı yollar](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview).

- **BGP yolları:** bir Azure VPN ağ geçidi veya ExpressRoute bağlantısı kullanarak VNet tooyour şirket içi ağınıza bağlanıyorsanız, BGP yolları tooyour sanal ağlar yayabilirsiniz.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>Karma Internet bağlantısı: tooan şirket içi ağa bağlan
Şirket içi ağ tooa seçenekleri aşağıdaki hello herhangi bir bileşimini kullanarak VNet bağlanabilir:

-   İnternet bağlantısı

-   Noktadan siteye VPN (P2S VPN)

-   Siteden siteye VPN (S2S VPN)

-   ExpressRoute

#### <a name="internet-connectivity"></a>Internet bağlantısı

Adından da anlaşılacağı gibi Internet bağlantısı iş yüklerinizi hello Internet'ten erişilebilir, hello sanal ağ içinde dinamik farklı ortak uç noktalar tooworkloads kullanıma sağlayarak yapar. Bu iş yükleri kullanarak açığa çıkabileceği [Internet'e yönelik Yük Dengeleyici](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) veya adres toohello VM yalnızca genel IP atama. Bu sanal makine herhangi bir şey hello Internet toobe mümkün tooreach üzerinde sağlanan için bir ana bilgisayar Güvenlik Duvarı bu şekilde, bu olası duruma [ağ güvenlik grubu (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), ve [kullanıcı tanımlı rotaları](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) , izin ver toohappen.

Bu senaryoda, toobe ortak toohello Internet gerektiren bir uygulama kullanıma ve herhangi bir yere veya iş yüklerinizin hello yapılandırmasına bağlı olarak belirli konumlardan gelen mümkün tooconnect tooit olması.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>Noktadan siteye VPN veya siteden siteye VPN
Bu iki düştüğünde içine aynı kategoride hello. Her ikisi de, VNet toohave bir VPN ağ geçidi gerekir ve bir VPN istemcisi için iş istasyonunuzu hello bir parçası olarak kullanma tooit bağlanabilir [noktadan siteye Yapılandırması](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) veya şirket içi yapılandırabilirsiniz [VPN cihazı](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe mümkün tooterminate bir siteden siteye VPN. Bu şekilde, şirket içi cihazları hello VNet içinde tooresources bağlanabilir.

Bir noktadan siteye (P2S) yapılandırması, bir tek bir istemci bilgisayar tooa sanal ağdan güvenli bir bağlantı oluşturmanızı sağlar. P2S, SSTP (Güvenli Yuva Tünel Protokolü) aracılığıyla gerçekleşen bir VPN bağlantısıdır.

![Noktadan siteye VPN](media/azure-network-security/azure-network-security-fig-5.png)

Giriş veya bir Konferanstan Merkezi'nden tooconnect tooyour uzak bir konumdan gibi istediğinizde ya da yalnızca tooconnect tooa sanal ağ gereken birkaç istemciniz bulunduğunda noktadan siteye bağlantıları faydalıdır.

P2S bağlantılarının bir VPN cihazına veya genel kullanıma yönelik bir IP adresine gerek yoktur. Merhaba istemci bilgisayardan hello VPN bağlantısı kurun. Bu nedenle, birçok şirket içi cihazlar ve bilgisayarlar tooyour Azure ağı kalıcı bir bağlantı gerektiğinde P2S şekilde tooconnect tooAzure önerilmez.

![Siteden siteye VPN](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> Noktadan siteye bağlantılar hakkında daha fazla bilgi için bkz: Merhaba [noktası siteye FA v Q](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal).

Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ.

Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir. Bu bağlantı gerçekleşmesi üzerinde Internet hello ve sağlar çok "ağınız ve Azure arasında şifrelenmiş bir bağlantı içindeki bilgileri tünel". Siteden siteye VPN ölçekteki kurumların on yılları için dağıtılan güvenli, olgun bir teknolojidir. Tünel şifreleme kullanarak gerçekleştirilir [IPSec tünel modu](https://technet.microsoft.com/library/cc786385.aspx).

Siteden siteye VPN güvenilir, güvenilir ve yerleşik bir teknoloji olsa da, hello tünel içindeki trafiği hello Internet çapraz geçiş. Ayrıca, bant genişliği görece kısıtlanmış tooa en fazla 200 MB/sn ' dir.

Şirket içi bağlantılarınız için güvenlik ve performans olağanüstü bir düzeyi gerekiyorsa, şirket içi bağlantılar için Azure ExpressRoute kullanmanızı öneririz. Expressroute'dur ayrılmış WAN şirket içi konumunuz veya bir Exchange barındırma sağlayıcısı arasındaki bağlantı. Bu telco bağlantı olduğundan, verilerinizi hello Internet yolculuk değil ve bu nedenle değil gösterilen toohello olası riskleri Internet iletişimlerde devralınmış.

> [!Note]
> VPN ağ geçitleri hakkında daha fazla bilgi için bkz: [VPN ağ geçidi](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).

#### <a name="dedicated-wan-link"></a>Ayrılmış bir WAN bağlantısı
Microsoft Azure ExpressRoute bağlantı sağlayıcı tarafından kolaylaştırılan adanmış özel bağlantı üzerinden Azure hello içine şirket içi ağlarınız genişletmenizi sağlar.

ExpressRoute bağlantıları hello Git değil genel Internet. Bu ExpressRoute bağlantıları toooffer daha fazla güvenilirlik, yüksek hız, düşük gecikme ve normal bağlantıları daha yüksek güvenlik hello Internet sağlar.

![ Ayrılmış bir WAN bağlantısı](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> Hakkında bilgi için tooconnect ExpressRoute kullanılarak, ağ tooMicrosoft bkz [ExpressRoute bağlantı modelleri](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) ve [ExpressRoute teknik genel bakış](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

Olarak hello siteden siteye VPN seçeneklerle ExpressRoute mutlaka yalnızca bir VNet içinde olmayan tooconnect tooresources sağlar. Aslında, SKU hello bağlı olarak, too10 sanal ağlara bağlanabilir. Merhaba varsa [premium eklentisi](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), bağlantıları tooup too100 Vnet'ler olası bağlı olarak bant genişliği. toolearn ne bağlantıları görünüm bu tür, okuma gibi hakkında daha fazla [bağlantı topoloji diyagramları](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="security-controls"></a>Güvenlik denetimleri
Bir Azure sanal ağı diğer sanal ağlardan yalıtılmış ve şirket içi ağlarınız kullanan çok sayıda güvenlik denetimleri destekleyen güvenli, mantıksal bir ağ sağlar. Müşteriler kullanarak kendi yapısı oluşturun: alt ağlar — bunlar, kendi özel IP adresi aralığı kullanın, yol tablolarını yapılandırmak, güvenlik grupları, ağ erişimi, iş yüklerini hello bulutta listeleri (ACL'ler), ağ geçitleri ve sanal gereçler toorun denetlemek.

Merhaba, güvenlik denetimleri, Azure sanal ağlarda kullanabilirsiniz şunlardır:

-   Ağ erişim denetimleri

-   Kullanıcı tanımlı yollar

-   Ağ güvenlik uygulaması

-   Application Gateway

-   Azure Web uygulaması güvenlik duvarı

-   Ağ kullanılabilirlik denetimi

#### <a name="network-access-controls"></a>Ağ erişim denetimleri
Hello Azure sanal ağ (VNet) Azure ağ modelinin hello dönüm ve yalıtım ve koruma sağlar, ancak hello [ağ güvenlik grupları (NSG)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) hello ana aracı ağ trafiğini tooenforce ve denetim kullanın Merhaba ağ düzeyinde kuralları.

![ Ağ erişim denetimleri](media/azure-network-security/azure-network-security-fig-8.png)


Erişimine izin verme veya reddetme hello iş yükleri bir sanal ağdan şirket içi bağlantılar aracılığıyla müşterinin ağlarındaki sistemleri arasındaki iletişimi tarafından erişimi denetlemek veya Internet iletişimi doğrudan.

Merhaba şemada hello Azure genel güvenlik yığınında Nsg'ler, UDR ve ağ sanal Gereçleri korumalı hello ağda kullanılan toocreate güvenlik sınırları tooprotect hello uygulama dağıtımları burada olabilir, belirli bir katmandaki sanal ağlar ve Nsg'ler bulunur.

Nsg'ler 5-tanımlama grubu tooevaluate trafik kullanın (ve yapılandırdığınız hello kurallarında NSG hello için kullanılır):

-   [Kaynak ve hedef IP adresi](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [Kaynak ve hedef bağlantı noktası](https://technet.microsoft.com/library/dd197515)

-   Protokol: [İletim Denetimi Protokolü (TCP)](https://technet.microsoft.com/library/cc940037.aspx) veya [kullanıcı veri birimi Protokolü (UDP)](https://technet.microsoft.com/library/cc940034.aspx)

Tek bir VM'ye ve bir grubu arasındaki erişimi denetleyebilir yani VM'ler veya tek bir VM tooanother VM, tek veya tüm alt ağlar arasında. Yeniden, bu filtreleme, basit durum bilgisi olan paket olan değil tam paket incelemesi unutmayın. Protokol doğrulama veya ağ düzeyi kimlik veya bir ağ güvenlik grubundaki IP'leri yeteneği yoktur.

Bir NSG'yi farkında olmanız gereken bazı yerleşik kurallar ile birlikte gelir. Bunlar:

-   **Belirli bir sanal ağ içindeki tüm trafiğe izin:** hello tüm sanal makinelerin aynı Azure sanal ağ iletişim kurabilir birbirleri ile.

-   **Azure Yük Dengeleme tooinbound izin ver:** bu kural hello Azure yük dengeleyici için herhangi bir kaynak adresi tooany hedef adresine gelen trafiği sağlar.

-   **Gelenlerin tümünü Reddet:** bu kural açıkça izin verdiğiniz Internet hello kaynak Hizmeti'nden tüm trafiği engeller.

-   **Tüm trafiği giden toohello Internet izin ver:** bu kural VM'ler tooinitiate bağlantıları toohello Internet izin verir. Bu bağlantılar başlatılan istemiyorsanız, bu bağlantılar toocreate kural tooblock gerekir veya zorlamalı tünel zorlamaz.

#### <a name="system-routes-and-user-defined-routes"></a>Sistem yollarıyla ve kullanıcı tanımlı yollar

Azure'da sanal makine (VM) tooa sanal ağ (VNet) eklediğinizde, hello VM'ler hello ağ üzerinden birbirleriyle mümkün toocommunicate otomatik olarak olduğuna dikkat edin. Merhaba VM'ler olsa da farklı alt ağlarda bir ağ geçidi toospecify gerekmez.

Merhaba aynı hello VM'ler toohello gelen iletişimi için doğru ortak Internet ve Azure tooyour karma bağlantısından sahip olduğunda datacenter varsa bile tooyour şirket içi ağ.

![Sistem Yolları](media/azure-network-security/azure-network-security-fig-9.png)

Azure bir dizi IP trafiğinin nasıl akacağını sistem yolları toodefine kullandığından bu iletişim akışını mümkündür. Sistem yolları senaryoları aşağıdaki hello iletişiminde hello akışını denetler:

-   Aynı alt ağ içinden hello.

-   Bir sanal ağ içindeki bir alt ağ tooanother.

-   Sanal makineleri toohello ' Internet.

-   Bir VNet tooanother sanal ağ VPN ağ geçidi üzerinden.

-   VNet tooanother VNet VNet eşlemesi aracılığıyla gelen ([hizmet zincirleme](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   VNet tooyour şirket içi ağ üzerinden bir VPN ağ geçidi üzerinden.

Çoğu işletmenin sıkı güvenlik vardır ve tüm ağ paketlerinin tooenforce belirli şirket içi incelenmesi gerektiren uyumluluk gereksinimlerine tanımlar. Azure adlı bir mekanizma sağlar [zorlanan tünel](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) özel bir yol oluşturarak veya hello VM'ler tooon içi trafiğinden yönlendirmeleri [sınır ağ geçidi Protokolü (BGP)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) reklamları ExpressRoute veya VPN.

Zorlamalı tünel Azure'da sanal ağ kullanıcı tanımlı yolları (UDR) yapılandırılır. Yeniden yönlendirme trafiği tooan site varsayılan yol toohello Azure VPN ağ geçidi olarak ifade edilir şirket içi.

Merhaba aşağıdaki bölümde bir Azure sanal ağı hello yönlendirme tablosuna ve yollar sınırlama geçerli hello listelenmektedir:

-   Her sanal ağ alt yerleşik sistem yönlendirme tablosu vardır. Merhaba sistem yönlendirme tablosu aşağıdaki üç grup yolların hello sahiptir:

 -  **Yerel VNet yollar:** doğrudan toohello hedef VM'ler hello aynı sanal ağ

 - **Şirket içi rota:** toohello Azure VPN ağ geçidi

 -  **Varsayılan yol:** doğrudan toohello Internet. Merhaba önceki iki yolları tarafından kapsanmayan hedefleyen paketler toohello özel IP adresleri bırakılır.

-   Kullanıcı tanımlı yolların Hello sürümle birlikte, bir yönlendirme tablosu tooadd varsayılan yol oluşturun ve bu alt ağlardaki tünel zorunlu hello yönlendirme tablosu tooyour sanal alt ağ tooenable ilişkilendirin.

-   Tooset "varsayılan site" Merhaba şirket içi yerel siteleri bağlı toohello sanal ağ arasında gerekir.

-   Zorlamalı tünel dinamik yönlendirme VPN ağ geçidi (olmayan bir statik ağ geçidi) sahip bir sanal ağ ile ilişkilendirilmiş olması gerekir.

- Zorlanan tünel ExpressRoute bu düzenek yapılandırılmamış, ancak bunun yerine, varsayılan rota hello ExpressRoute BGP üzerinden reklam tarafından etkinleştirilmiş eşliği oturumlarını.

> [!Note]
> Daha fazla bilgi için bkz: Merhaba [ExpressRoute belgeleri](https://azure.microsoft.com/documentation/services/expressroute/) daha fazla bilgi için.

#### <a name="network-security-appliances"></a>Ağ güvenlik uygulamaları
Ağ güvenlik grupları ve kullanıcı tanımlı rotaları belirli bir ölçü ağ güvenlik hello en hello ağ ve Aktarım katmanı sağlayabilir sırada [OSI modeli](https://en.wikipedia.org/wiki/OSI_model), istediğiniz veya tooenable ihtiyacınız olduğu toobe durumlar olan gitme Merhaba ağ yığınının yüksek düzeyde güvenlik. Böyle durumlarda, Azure iş ortakları tarafından sağlanan sanal ağ güvenlik Gereçleri dağıtmanızı öneririz.

![Ağ güvenlik uygulamaları](./media/azure-network-security/azure-network-security-fig-10.png)

VNet güvenlik ve ağ işlevlerini Azure ağ güvenliği uygulamaları geliştirmek ve hello üzerinden çok sayıda satıcılardan kullanılabilir [Azure Marketi](https://azuremarketplace.microsoft.com). Bu sanal güvenlik Gereçleri dağıtılan tooprovide olabilir:

-   Yüksek oranda kullanılabilir güvenlik duvarları

-   Yetkisiz erişim önleme

-   Yetkisiz erişim algılama

-   Web uygulaması Güvenlik Duvarı (WAFs)

-   WAN iyileştirmesi

-   Yönlendirme

-   Yük dengeleme

-   VPN

-   Sertifika yönetimi

-   Active Directory

-   Çok faktörlü kimlik doğrulama

#### <a name="application-gateway"></a>Uygulama ağ geçidi

[Microsoft Azure uygulama ağ geçidi](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) uygulama teslim denetleyicisi (ADC) bir hizmet olarak sunar ayrılmış bir sanal gereç olduğu.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-11.png)

Uygulama ağ geçidi toooptimize web grubu performans ve kullanılabilirlik CPU yoğunluklu SSL sonlandırma toohello uygulama ağ geçidi (SSL boşaltma) boşaltarak sağlar. Ayrıca, dahil olmak üzere diğer katman 7 Yönlendirme yetenekleri sağlar:

-   Gelen trafiğin hepsini dağıtım

-   Tanımlama bilgisi tabanlı oturum benzeşimi

-   URL yolu tabanlı yönlendirme

-   Özelliği toohost tek bir uygulama ağ geçidi arkasında birden çok Web sitesi


A [web uygulaması Güvenlik Duvarı (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) de hello uygulama ağ geçidi bir parçası olarak sağlanır. Bu, ortak web Güvenlik Açıkları ve güvenlik açıklarına tooweb uygulamalardan koruma sağlar. Uygulama ağ geçidi, ağ geçidi, iç yalnızca ağ geçidi veya her ikisinin birleşimini Internet'e yönelik yapılandırılabilir.

Uygulama ağ geçidi WAF algılama veya önleme modda çalıştırabilirsiniz. Yöneticiler toorun algılama modunu tooobserve trafiğinin kötü amaçlı düzenleri için ortak bir kullanım örneği içindir. Olası açıkları algılanan sonra dönüş tooprevention modu şüpheli gelen trafiği engeller.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-12.png)

Ayrıca, uygulama ağ geçidi WAF web uygulamaları ile tümleşik gerçek zamanlı WAF günlüğünü kullanarak saldırılarına karşı izlemenize yardımcı [Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) ve [Azure Güvenlik Merkezi](https://azure.microsoft.com/services/security-center/) tootrack WAF uyarıları ve kolayca eğilimlerini izleyin.

Merhaba biçimlendirilmiş JSON günlük doğrudan toohello müşterinin depolama hesabı gider. Bu günlükler üzerinde tam denetime sahiptir ve kendi bekletme ilkeleri uygulayabilirsiniz.

Kullanarak kendi analytics sistem Bu günlükler işleyebilen [Azure günlük tümleştirme](https://aka.ms/AzLog). WAF günlükleri ile tümleşik de [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) OMS günlük analizi kullanabilmeniz için tooexecute, Gelişmiş bir ayrıntılı sorgular.

#### <a name="azure-web-application-firewall-waf"></a>Azure web uygulaması Güvenlik Duvarı (WAF)

Web uygulamaları olan giderek SQL ekleme, siteler arası komut dosyası saldırıları ve hello görünen diğer saldırıları gibi ortak bilinen güvenlik açıklarından faydalanır kötü amaçlı saldırıları hedefleri [OWASP ilk 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). Bu tür açıkları hello uygulamada önleme düzeltme eki uygulama ve hello uygulama topolojisinin birden çok katmanına izleme sıkı bakım gerektirir.

 ![Azure Web uygulaması Güvenlik Duvarı (WAF)](./media/azure-network-security/azure-network-security-fig-13.png)

Bir merkezi [web uygulaması Güvenlik Duvarı (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) web saldırılarına karşı korumak ve uygulama değişiklikleri gerek kalmadan güvenlik yönetimini basitleştirir.

WAF Çözüm Merkezi bir konumda her tek tek web uygulamalarının güvenliğini sağlama karşı bilinen bir güvenlik açığı düzeltme eki uygulama tarafından tooa güvenlik tehdidi daha hızlı ayrıca tepki. Mevcut uygulama ağ geçitleri dönüştürülmüş tooa web uygulaması Güvenlik Duvarı etkin uygulama ağ geçidi kolayca olabilir.

#### <a name="network-availability-controls"></a>Ağ kullanılabilirliğini denetimleri

Microsoft Azure kullanarak farklı seçenekler toodistribute ağ trafiğini vardır. Bu seçenekler birbirlerinden farklı şekilde çalışır, farklı özelliklere sahiptir ve farklı senaryoları destekler. Birbirlerinden ayrı olarak veya birleştirilerek kullanılabilirler.

Aşağıdaki ağ kullanılabilirliği denetimleri hello:

-   Azure Load Balancer

-   Application Gateway

-   Traffic Manager

**Azure yük dengeleyici**

Yüksek kullanılabilirlik ve ağ performansı tooyour uygulamalar sunar. Gelen trafiği yükü dengelenmiş bir kümede tanımlanmış Hizmetleri sağlıklı örnekleri arasında dağıtır bir katman 4 (TCP, UDP) yük dengeleyici olur.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Azure yük dengeleyici için yapılandırılabilir:

-   Gelen Internet trafiği toovirtual makinelerin yük dengelemesini. Bu yapılandırma olarak bilinir [Internet'e yönelik Yük Dengeleme](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Yük Dengeleme trafiği sanal ağ içindeki sanal makineler arasında bulut Hizmetleri içindeki sanal makineler arasında veya şirket içi bilgisayarlar ve bir şirket içi sanal ağdaki sanal makineler arasında. Bu yapılandırma olarak bilinir [iç Yük Dengeleme](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview).

-   Dış trafiğin tooa belirli bir sanal makine iletin.

Merhaba buluttaki tüm kaynaklara bir ortak IP adresi toobe hello Internet erişilebildiğini gerekir. azure'da Hello bulut altyapısı için kaynaklarını yönlendirilebilir olmayan IP adreslerini kullanır. Azure ortak IP adresleri toocommunicate toohello ile Internet ağ adresi çevirisi (NAT) kullanır.

 **Uygulama ağ geçidi**

 Uygulama ağ geçidi hello uygulama katmanında (Merhaba OSI Ağ başvurusu yığınında katman 7) çalışır. Merhaba istemci bağlantısı kesiliyor bir ters proxy hizmeti davranır ve iletme tooback uç uç noktaları ister.

 **Trafik Yöneticisi**

Microsoft Azure trafik Yöneticisi toocontrol hello hizmet uç noktaları için kullanıcı trafiğinin dağıtımını farklı veri merkezlerinde sağlar. Trafik Yöneticisi tarafından desteklenen hizmet uç noktaları ve bulut hizmetlerini Azure VM'ler, Web uygulamaları içerir. Traffic Manager’ı harici, Azure dışı uç noktalar için de kullanabilirsiniz.

Trafik Yöneticisi kullanan etki alanı adı sistemi (DNS) toodirect istemci istekleri göre en uygun toohello uç nokta hello bir [trafik yönlendirme yöntemini](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) ve hello uç noktaları hello sistem durumu. Trafik Yöneticisi sağlayan bir dizi trafik yönlendirme yöntemleri toosuit farklı, uygulama gereksinimlerinde uç nokta durumu [izleme](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)ve otomatik yük devretme. Trafik, tüm bir Azure bölgesi hello başarısızlığını dahil esnek toofailure yöneticisidir.

Azure trafik Yöneticisi, uygulama uç noktalar arasında trafiği toocontrol hello dağıtımını sağlar. Bir uç nokta içinde veya Azure dışında barındırılan tüm Internet'e hizmetidir.

Trafik Yöneticisi iki temel fayda sağlar:

-   Birkaç tooone göre trafiğinin dağıtımını [trafik yönlendirme yöntemleri](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods).

-   [Sürekli uç noktası durumunu izleme](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) ve uç noktaları başarısız olduğunda otomatik yük devretme.

Bir istemci tooconnect tooa hizmeti çalıştığında, ilk hello DNS adı hello hizmet tooan IP adresi çözmeniz gerekir. Merhaba istemci ardından toothat IP adresi tooaccess hello hizmeti bağlanır. Trafik Yöneticisi kullandığı DNS toodirect istemcileri toospecific hizmet uç noktaları hello trafik yönlendirme yönteminin hello kurallara göre. İstemcileri seçili toohello uç noktası doğrudan bağlanın. Trafik Yöneticisi, bir proxy veya ağ geçidi değil. Trafik Yöneticisi hello istemciyle hello hizmeti arasında geçen hello trafiğine görmez.

### <a name="azure-network-validation"></a>Azure ağı doğrulama

Azure ağı doğrulama olan Azure ağ hello tooensure olarak yapılandırıldığından ve doğrulama yapılabilir işletim hello hizmetlerini ve özellikleri kullanılabilir toomonitor hello ağ kullanma. Azure Ağ İzleyicisi ile günlük sayısız erişebilir ve ağ performansı ve sistem durumu ile Öngörüler toounderstand güçlendirmeniz tanılama yetenekleri. Bu özellikler, Portal, Power Shell, CLI, Rest API ve SDK erişilebilir.

Azure işlem güvenliği verilerini, uygulamaları ve diğer Microsoft Azure varlıkları korumak için toohello Hizmetleri, denetimleri ve özellikler kullanılabilir toousers ifade eder. Azure işlem güvenliği hello Microsoft Security Development Lifecycle (SDL), Microsoft Güvenlik Yanıt Merkezi hello dahil olmak üzere benzersiz tooMicrosoft olan üzerinden çeşitli özellikleri elde edilen hello bilgi içeren bir çerçevesi üzerine inşa edilmiştir Program ve hello siber güvenlik tehdit derin tanıma.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Azure Ağ İzleyicisi](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Azure depolama çözümlemeleri](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Azure Resource Manager

#### <a name="azure-resource-manager"></a>Azure Kaynak Yöneticisi

Merhaba kişiler ve Microsoft Azure çalışan işlemleri belki de hello en önemli güvenlik hello platform özelliğidir. Bu bölümde geliştirmek ve güvenlik, sürekliliği ve gizlilik korumanıza yardımcı Microsoft'un küresel veri merkezi altyapı özelliklerini açıklar.

Uygulamanız için Hello altyapısı genellikle birçok bileşenlerinin – belki de bir sanal makine, depolama hesabı ve sanal ağ veya bir web uygulaması, veritabanı, veritabanı sunucusu ve üçüncü taraf hizmetleri oluşur. Bu bileşenleri ayrı varlıklar olarak değerlendirmez, bunun yerine bunları tek bir varlığın ilgili ve birbirine bağımlı parçaları olarak kabul edersiniz. Toodeploy istediğiniz, yönetmek ve bunları bir grup olarak izleyebilirsiniz. Azure Resource Manager toowork çözümünüzdeki hello kaynaklarla bir grup olarak sağlar.

Dağıtma, güncelleştirme veya tek ve eşgüdümlü bir işlemle, çözümünüz için tüm hello kaynakları silin. Dağıtım için bir şablon kullanabilirsiniz. Üstelik bu şablon test, hazırlık ve üretim gibi farklı ortamlarda da çalışabilir. Resource Manager Güvenlik denetimi sağlar ve özellikleri toohelp etiketleme, kaynaklarınızın dağıtımdan sonra yönetin.

**Kaynak Yöneticisi'ni kullanarak hello avantajları**

Resource Manager çeşitli avantajlar sunar:

-   Dağıtmak, yönetmek ve bir grubu yerine bu kaynakları ayrı ayrı ele çözümünüz için tüm hello kaynakları izle.

-   Art arda çözümünüzü hello geliştirme yaşam döngüsü boyunca dağıtmak ve kaynaklarınızın tutarlı bir durumda dağıtılması da size güven verir.

-   Altyapınızı betikler yerine bildirim temelli şablonları kullanarak yönetebilirsiniz.

-   Merhaba doğru sırayla dağıtılmalarını sağlamak kaynakları arasındaki hello bağımlılıkları tanımlayabilirsiniz.

-   Rol tabanlı erişim denetimi (RBAC) yerel olarak hello yönetim platformuyla doğrudan tümleşik olduğundan, kaynak grubuna erişim denetimi tooall Hizmetleri uygulayabilirsiniz.

-   Etiketleri uygulayabilirsiniz tooresources toologically aboneliğinizdeki tüm hello kaynakları düzenleyin.

-   Etiketi paylaşan kaynak grubu için maliyetleri görüntüleyerek kuruluşunuzun fatura açıklık getirebilir.

> [!Note]
> Resource Manager çözümlerinizi yönetmek ve yeni bir yolu toodeploy sağlar. Kullandıysanız Merhaba önceki dağıtım modelini ve hello değişiklikler hakkında toolearn istediğiniz, bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="azure-network-logging-and-monitoring"></a>Azure ağı günlüğe kaydetme ve izleme

Azure birçok araçları toomonitor sunar, engellemek, algılamak ve toonetwork güvenlik olaylarına yanıt. Merhaba en güçlü araçlar kullanılabilir tooyou bu alandaki bazıları şunlardır:

-   Ağ İzleyicisi

-   Ağ kaynak düzeyi izleme

-   Log Analytics

### <a name="network-watcher"></a>Ağ İzleyicisi

[Ağ İzleyicisi](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -senaryo tabanlı izleme Ağ İzleyicisi Merhaba özellikleriyle sağlanır. Bu hizmet içeren paket yakalama, sonraki atlama IP akış, güvenlik grubu görünümü, NSG akış günlükleri doğrulayın. Senaryo düzeyi izleme Karşıtlık tooindividual ağ kaynak izleme ağ kaynaklarına bir uçtan tooend görünümünü sağlar.

 ![Ağ İzleyicisi](./media/azure-network-security/azure-network-security-fig-15.png)

Ağ İzleyicisi'ni ve koşullar bir ağ düzeyinde senaryo içinde gelen ve giden Azure Tanılama, toomonitor sağlayan bölgesel bir hizmettir. Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Öngörüler tooyour Azure ağında geçirmesine yardımcı olur.

Ağ İzleyicisi'ni şu anda özellikleri aşağıdaki hello sahiptir:

#### <a name="topology"></a>Topoloji

[Topoloji](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) bir sanal ağda ağ kaynaklarının bir grafik döndürür. Merhaba grafikte hello bağlantısı hello kaynakları toorepresent hello son tooend ağ bağlantısı arasında gösterilmektedir. Merhaba Portalı'nda topoloji hello kaynak nesneleri sanal ağ temeli başına döndürür. Merhaba kaynak grubu görüntülenmeyecek olsa bile hello Ağ İzleyicisi bölgesi dışında hello kaynaklar arasındaki çizgilerle hello ilişkileri gösterilen. Merhaba portal görünümünde döndürülen hello kaynakları grafiği çizilecek hello ağ bileşenleri bir alt kümesidir. ağ kaynakları toosee hello tam listesi, kullanabileceğiniz [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) veya [REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest).

Kaynakları döndürülen bunlar arasında hello bağlantısı Modellenen altında iki ilişki.

- **Kapsama** -sanal ağ, bir NIC içeren bir alt ağ içerir

- **İlişkili** -A NIC, bir VM ile ilişkilendirilmiş.

#### <a name="variable-packet-capture"></a>Değişken paket yakalama

Ağ İzleyicisi [değişken paket yakalama](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) toocreate paket yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar. Paket yakalama toodiagnose ağ anormallikleri hem Tepkisel yardımcı olur ve proactivity. Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir.

Paket yakalama Ağ İzleyicisi uzaktan başlatılan bir sanal makine uzantısıdır. Bu özellik, bir paket yakalama istenen hello sanal değerli zaman kazandırır makineye el ile çalışan hello yük kolaylaştırır. Paket yakalama hello portal, PowerShell'i, CLI veya REST API tetiklenebilir. Paket yakalama nasıl tetiklenebilir bir sanal makine uyarılara örnektir.

#### <a name="ip-flow-verify"></a>IP akış doğrulayın

[IP akışları doğrulayın](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) bir paket izin verilen veya 5-tanımlama bilgilerine dayalı bir sanal makineden tooor reddedildi olup olmadığını denetler. Bu bilgiler yönü, protokol, yerel IP, uzak IP, yerel bağlantı noktası ve uzak bağlantı noktası oluşur. Başlangıç paketi bir güvenlik grubu tarafından engellenirse hello Paket reddedildi hello kuralının hello adı döndürülür. Bu özellik, kaynak veya hedef IP seçilebilir durumdayken, yöneticilerin gelen bağlantı sorunları veya toohello bulmanıza yardımcı olur Internet ve veya toohello şirket içi ortamda.

IP akışları doğrulayın hedefleyen bir sanal makinenin ağ arabirimi. Trafik akışı yapılandırılmış hello ayarları tooor bu ağ arabiriminden göre doğrulanır. Bu özellik, bir ağ güvenlik grubu kural bir sanal makineden giriş ve çıkış trafiği tooor durumunda engelliyor onaylayan yararlıdır.

#### <a name="next-hop"></a>Sonraki atlama

Merhaba belirler [sonraki atlama](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) hello Azure ağ Fabric yönlendirilen paketler için toodiagnose her etkinleştirme kullanıcı tanımlı yollar yanlış yapılandırılmış. Bir VM'ye gelen trafiği tooa hedef bir NIC ile ilişkili hello etkili rotalarını göre gönderilir Sonraki atlama hello sonraki atlama türü ve IP adresi bir paket için bir belirli bir sanal makine ve NIC alır Bu hello paket yönlendirilmiş toohello hedef yüklenmekte olan veya siyah olan hello trafiği holed toodetermine yardımcı olur.

Sonraki atlama ayrıca hello sonraki atlama ile ilişkili hello yol tablosu döndürür. Bu rota Hello rota kullanıcı tanımlı bir yol olarak tanımlanırsa, bir sonraki atlama sorgulanırken döndürülür. Aksi takdirde sonraki atlama "Sistem yolu" döndürür.

#### <a name="security-group-view"></a>Güvenlik grubu görünümü

Bir VM üzerinde uygulanan hello etkili ve uygulanan güvenlik kuralları alır. Ağ güvenlik grupları, bir alt ağ düzeyinde veya bir NIC düzeyi ilişkilendirilir. Bir alt düzeyde ilişkili hello alt ağdaki tooall hello VM örnekleri uygulanır. Ağ [güvenlik grubu görünümü](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) tüm yapılandırılmış hello Nsg'ler ve hello yapılandırma hakkında bilgi sağlayan bir sanal makine için bir NIC ve alt ağ düzeyinde ilişkili kurallar döndürür. Ayrıca, her bir VM hello NIC hello etkin güvenlik kuralları döndürülür. Ağ güvenlik grubu kullanarak görünüm açık bağlantı noktaları gibi ağ güvenlik açıkları için bir VM değerlendirebilirsiniz. De doğrulamak, ağ güvenlik grubu temel alarak beklendiği gibi çalışıp çalışmadığını bir [hello karşılaştırması yapılandırılmış ve etkin güvenlik kuralları hello](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell).

#### <a name="nsg-flow-logging"></a>NSG akış günlüğe kaydetme

 Akış günlükleri ağ güvenlik grupları için izin verilen veya hello Grup hello güvenlik kuralları tarafından reddedilen toocapture günlükleri ilgili tootraffic sağlar. Merhaba akışı bir 5-tanımlama grubu bilgileriyle – kaynak IP, hedef IP, kaynak bağlantı noktası, hedef bağlantı noktası ve protokol tanımlanır.

[Ağ güvenlik grubu akış günlükleri](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi bir özelliğidir.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Sanal ağ geçidi ve bağlantı sorunlarını giderme

Ağ kaynaklarınızı Azure toounderstanding ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar. Bu özelliklerin biri kaynak sorun giderme. [Kaynak sorun giderme](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) PowerShell'i, CLI veya REST API tarafından çağrılabilir. Çağrıldığında, Ağ İzleyicisi Merhaba bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.

Bu bölüm kaynak sorun giderme için şu anda kullanılabilir hello farklı yönetim görevleri yoluyla alır.

-   [Bir sanal ağ geçidi sorun giderme](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [Bir bağlantı sorunlarını giderme](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>Ağ abonelik sınırları

[Ağ abonelik sınırları](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) her bir abonelikte kullanılabilir kaynakları hello sayısının karşı bir bölgede hello ağ kaynağının hello kullanım ayrıntılarını sağlar.

#### <a name="configuring-diagnostics-log"></a>Tanılama günlük yapılandırma

Ağ İzleyicisi sağlayan bir [tanılama günlüklerini](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) görünümü. Bu görünüm, tanılama günlüğünün destekleyen tüm ağ kaynaklarını içerir. Bu görünümden etkinleştirin ve ağ kaynaklarını kolayca ve hızlı bir şekilde devre dışı bırakın.

### <a name="network-resource-level-monitoring"></a>Ağ kaynak düzeyi izleme

özellikler aşağıdaki Merhaba, kaynak düzeyi izleme için kullanılabilir:

#### <a name="audit-log"></a>Denetim günlüğü

Ağların hello yapılandırmasının bir parçası gerçekleştirilen işlemleri günlüğe kaydedilir. Bu denetim günlükleri temel tooestablish çeşitli compliances şunlardır. Bu günlükler hello Azure portal görüntülenebilir veya Power BI gibi Microsoft araçları veya üçüncü taraf araçlarını kullanarak alınamıyor. Denetim günlüklerini hello portal, PowerShell'i, CLI ve Rest API kullanılabilir.

> [!Note]
> Denetim günlükleri hakkında daha fazla bilgi için bkz: [denetim işlemleri Resource Manager ile](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
Denetim günlükleri, tüm ağ kaynaklarına yapılan işlemleri için kullanılabilir.


#### <a name="metrics"></a>Ölçümler

Performans ölçümleri ve belirli bir süre boyunca toplanan sayaçları ölçümleridir. Ölçümleri uygulama ağ geçidi için şu anda kullanılabilir. Ölçümleri kullanılan tootrigger uyarıları eşiğine dayalı olabilir. Varsayılan olarak Azure uygulama ağ geçidi arka uç havuzundaki tüm kaynakları hello durumunu izler ve hello havuzundan sağlıksız kabul herhangi bir kaynağa otomatik olarak kaldırır. Uygulama ağ geçidi toomonitor hello sağlıksız örnekleri devam eder ve bunları ekler kullanılabilir durumda olduklarında ve yanıt toohealth yoklamaları sonra toohello sağlıklı arka uç havuzu yedekleyin. Uygulama ağ geçidi hello sistem durumu araştırmalarının hello ile Merhaba arka uç HTTP Ayarları'nda tanımlanan aynı bağlantı noktasını gönderir. Bu yapılandırma bu hello araştırma müşteriler tooconnect toohello arka uç kullanarak, aynı bağlantı noktası hello sınama sağlar.

> [!Note]
> Bkz: [uygulama ağ geçidi tanılama](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview ölçümleri kullanılan toocreate uyarıları nasıl olabilir.

#### <a name="diagnostic-logs"></a>Tanılama günlükleri

Dönemsel ve spontaneous olayları ağ kaynakları tarafından oluşturulan ve gönderilen tooan olay hub'ı ya da günlük analizi depolama hesaplarında oturum. Bu günlükleri bir kaynak hello durumunu fikir sağlar. Bu günlükler Power BI ve günlük analizi gibi araçları görüntülenebilir. nasıl tooview tanılama günlükleri, ziyaret toolearn [günlük analizi](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics).

Tanılama günlükleri için kullanılabilir [yük dengeleyici](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [ağ güvenlik grupları](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), yollar ve [uygulama ağ geçidi](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Ağ İzleyicisi görünümü bir tanılama günlükleri sağlar. Bu görünüm, tanılama günlüğünün destekleyen tüm ağ kaynaklarını içerir. Bu görünümden etkinleştirin ve ağ kaynaklarını kolayca ve hızlı bir şekilde devre dışı bırakın.

### <a name="log-analytics"></a>Log Analytics

[Günlük analizi](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) bir hizmetidir [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) , performans ve kullanılabilirlik, Bulut ve şirket içi ortamları toomaintain izler. Bulut ve şirket içi ortamları ve diğer izleme araçları tooprovide analiz kaynaklar tarafından birden çok kaynakları genelinde oluşturulan veri toplar.

Günlük analizi çözümleri, ağları izleme için aşağıdaki hello sunar:

-   Ağ Performans İzleyicisi'ni (NPM)

-   Azure uygulama ağ geçidi analizi

-   Azure ağ güvenlik grubu analizi

#### <a name="network-performance-monitor-npm"></a>Ağ Performans İzleyicisi'ni (NPM)
Merhaba [Ağ Performansı İzleyicisi](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) yönetimi çözümüdür ağ hello sistem durumu, kullanılabilirlik ve ulaşılabilirlik ağların izler çözüm izleme.

Arasında kullanılan toomonitor bağlantısı şöyledir:

-   Genel Bulut ve şirket içi

-   veri merkezleri ve kullanıcı konumları (şubelere)

-   çok katmanlı bir uygulama çeşitli katmanlarını barındırma alt ağlar.


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Azure uygulama ağ geçidi analizleri günlük analizi

Uygulama ağ geçitleri için günlükleri aşağıdaki hello desteklenir:

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

Ölçümleri aşağıdaki hello uygulama ağ geçitleri için desteklenir:

-   5 dakikalık işleme

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Azure ağ güvenlik grubu analizleri günlük analizi

Merhaba günlükleri için desteklenen [ağ güvenlik grubu](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:** için hangi NSG kuralları: uygulanan tooVMs ve örnek rolleriniz MAC adresine dayalı girişleri içerir. Bu kurallar Hello durumunun her 60 saniyede toplanır.

- **NetworkSecurityGroupRuleCounter:** kaç kez her NSG için içerir girişleri kural uygulanan toodeny ya da trafiğine izin verme.

## <a name="next-steps"></a>Sonraki adımlar
Güvenlik hakkında daha fazla bizim kapsamlı güvenlik konuların bazıları okuyarak bulun:

-   [Ağ güvenlik grupları (Nsg'ler) için günlük analizi](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [Bu sürücü hello bulut kesintisi yenilikleri ağ oluşturma](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [SONiC: ağ hello Microsoft Genel bulut'ın temelini oluşturan anahtar yazılımı hello](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Microsoft, hızlı ve güvenilir bir genel ağ nasıl oluşturulur](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [Aydınlatma ağ yenilik ayarlama](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
