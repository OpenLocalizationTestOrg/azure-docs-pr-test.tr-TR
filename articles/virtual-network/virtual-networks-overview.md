---
title: "Sanal ağ aaaAzure | Microsoft Docs"
description: "Azure Virtual Network kavramları ve özellikler hakkında bilgi edinin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Azure Sanal Ağ

Merhaba, toosecurely bağlanmak tooeach Azure kaynaklarını diğer sanal ağlar (Vnet'ler) ile Azure Virtual Network service etkinleştirir. Bir VNet kendi ağ hello bulutta gösterimidir. Bir VNet hello ayrılmış Azure bulut tooyour abonelik mantıksal yalıtımının ' dir. Ayrıca, sanal ağlar tooyour şirket ağına bağlanabilir. Resim aşağıdaki hello bazı hello Azure Virtual Network service hello özelliklerini gösterir:

![Ağ Diyagramı](./media/virtual-networks-overview/virtual-network-overview.png)

toolearn hakkında daha fazla Azure sanal ağ özellikleri, aşağıdaki hello hello yetenek tıklatın:
- **[Yalıtım:](#isolation)**  sanal ağlar birbirinden yalıtılmış. Bu kullanım hello geliştirme, test ve üretim için ayrı sanal ağlar oluşturabilirsiniz aynı CIDR adres bloklarını. Buna karşılık, ağları birbirine bağlamak ve farklı CIDR adres bloklarını kullanan birden çok sanal ağlar oluşturabilirsiniz. Bir sanal ağ birden çok alt ağa bölebilirsiniz. Azure VM'ler için dahili ad çözümlemesi sağlar ve bulut Hizmetleri rol örnekleri tooa VNet bağlı. Bu gibi durumlarda, bir VNet toouse isteğe bağlı olarak Azure dahili ad çözümlemesi yerine kendi DNS sunucularınızı yapılandırabilirsiniz.
- **[Internet bağlantısı:](#internet)**  bağlı tooa VNet sahip tüm Azure sanal makineler (VM) ve bulut Hizmetleri rol örnekleri varsayılan toohello Internet erişim. Gelen erişim toospecific kaynakları, gerektiğinde de etkinleştirebilirsiniz.
- **[Azure kaynak bağlantısı:](#within-vnet)**  bulut Hizmetleri ve sanal makineleri gibi Azure kaynakları bağlı toohello olabilir aynı sanal ağı. Merhaba kaynakları tooeach diğer bağlanabilir özel IP adresleri, farklı alt ağlarda olsalar bile. Azure yoksa tooconfigure ve yollar yönetmek için varsayılan alt ağlar, sanal ağlar ve şirket içi ağlar arasında yönlendirme sağlar.
- **[VNet bağlantısı:](#connect-vnets)**  sanal ağlar, diğer bağlı tooeach olabilir, kaynakları etkinleştirme bağlı tooany VNet toocommunicate başka bir VNet üzerinde herhangi bir kaynağa sahip.
- **[Şirket içi bağlantı:](#connect-on-premises)**  sanal ağlar hello Internet ağınız ve Azure arasında özel ağ bağlantıları üzerinden veya siteden siteye VPN bağlantısı üzerinden bağlı tooon içi ağlar olabilir.
- **[Trafik filtreleme:](#filtering)**  VM ve bulut Hizmetleri rol örneklerini ağ trafiği filtre gelen ve giden kaynak IP adresi ve bağlantı noktası, hedef IP adresi ve bağlantı noktası ve protokolü tarafından.
- **[Yönlendirme:](#routing)**  isteğe bağlı olarak, kendi yolları yapılandırmak veya bir ağ geçidi üzerinden BGP yollarını kullanarak yönlendirme Azure'un varsayılan ayarlarını geçersiz kılabilir.

## <a name = "isolation"></a>Ağ yalıtımı ve kesimleme

Her Azure içinde birden çok sanal ağlar uygulayabilirsiniz [abonelik](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) ve Azure [bölge](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region). Her sanal ağ, diğer sanal ağlardan yalıtılır. Her sanal ağ için şunları yapabilirsiniz:
- Ortak ve özel (RFC 1918) adreslerini kullanarak özel bir özel IP adres alanını belirtin. Azure kaynakları bağlı toohello VNet hello adres alanından atadığınız özel bir IP adresi atar.
- Bir veya daha fazla alt ağ içinde Hello VNet segmentlere ayırmak ve hello sanal adres alanı tooeach alt kısmı paylaştırabilirsiniz.
- Azure tarafından sağlanan ad çözümlemesi kullanın veya kaynaklar tarafından kullanılmak üzere kendi DNS sunucusu tooa VNet bağlı belirtin. Merhaba okuma vnet'lerdeki ad çözümlemesi hakkında daha fazla toolearn [VM'ler ve bulut Hizmetleri için ad çözümlemesi](virtual-networks-name-resolution-for-vms-and-role-instances.md) makalesi.

## <a name = "internet"></a>Toohello Internet Bağlan
Tüm kaynaklara bağlı tooa VNet varsayılan giden bağlantı toohello Internet vardır. Merhaba özel IP adresi hello kaynağının kaynak ağ adresi (SNAT) tooa genel IP adresi hello Azure altyapısı tarafından çevrilen değil. toolearn hello okuma giden Internet bağlantısı hakkında daha fazla [azure'da giden bağlantılar anlama](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address) makalesi. Özel Yönlendirme ve trafik filtreleme uygulayarak hello varsayılan bağlantı değiştirebilirsiniz.

toocommunicate Internet SNAT, bir kaynak olmadan genel bir IP adresi atanmalıdır hello Internet ya da toocommunicate giden toohello tooAzure kaynaklardan gelen. Merhaba okuma genel IP adresleri hakkında daha fazla toolearn [ortak IP adresleri](virtual-network-public-ip-address.md) makalesi.

## <a name="within-vnet"></a>Azure kaynaklarına bağlanma
Birkaç Azure kaynaklarını tooa sanal makineler (VM), bulut Hizmetleri, uygulama hizmeti ortamları ve sanal makine ölçek kümeleri gibi VNet bağlanabilir. VM'ler tooa alt ağ bir sanal ağ içindeki ağ arabirimi (NIC) üzerinden bağlanır. NIC'ler, hello okuma hakkında daha fazla toolearn [ağ arabirimleri](virtual-network-network-interface.md) makalesi.

## <a name="connect-vnets"></a>Sanal ağlara bağlanabilir

Sanal ağlar tooeach diğer bağlanabilir, kaynakları etkinleştirme tooeither VNet toocommunicate birbirleri ile sanal ağlar bağlanır. Veya her ikisini seçenekleri tooconnect sanal ağlar tooeach diğer aşağıdaki hello kullanabilirsiniz:
- **Eşliği:** etkinleştirir kaynaklara bağlı hello içinde toodifferent Azure Vnet birbiriyle aynı Azure konumuna toocommunicate. Merhaba kaynaklara bağlı toohello değilmiş gibi hello bant genişliği ve gecikme hello olup Vnet'ler arasında aynı hello aynı sanal ağı. eşleme, hakkında daha fazla toolearn okuma hello [sanal ağ eşlemesi](virtual-network-peering-overview.md) makalesi.
- **VNet-VNet bağlantısı:** etkinleştirir kaynaklara bağlı toodifferent Azure VNet hello içinde aynı veya farklı Azure konumu. Bir Azure VPN ağ geçidi üzerinden trafik akışı gerekir çünkü eşliği farklı olarak, bant genişliği sanal ağlar arasında sınırlıdır. Merhaba okuma bir VNet-VNet bağlantısı ile sanal ağlara bağlanma hakkında daha fazla toolearn [VNet-VNet bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.

## <a name="connect-on-premises"></a>Tooan şirket içi ağa bağlan

Şirket içi ağ tooa seçenekleri aşağıdaki hello herhangi bir bileşimini kullanarak VNet bağlanabilir:
- **Noktadan siteye sanal özel ağ (VPN):** bir tek PC bağlı tooyour ağ ile Merhaba VNet arasında kuruldu. Çok az kayıpla veya hiç değişiklik tooyour mevcut ağ gerektirdiğinden bu bağlantı türü, yalnızca Azure ile ya da geliştiricileri için başlıyorsanız mükemmeldir. Merhaba bağlantı hello SSTP Protokolü şifrelenmiş tooprovide iletişimi hello PC ve hello VNet arasında hello Internet üzerinden kullanır. bir noktadan siteye VPN için hello gecikme Hello trafiğin hello Internet geçeceğini öngörülemeyen, taşımaktadır.
- **Siteden siteye VPN:** VPN cihazınız arasındaki bir Azure VPN ağ geçidi kuruldu. Bu bağlantı türü tooaccess VNet yetkilendirmek herhangi bir şirket içi kaynak sağlar. Merhaba, şirket içi cihaz hello Azure VPN ağ geçidi arasındaki hello Internet üzerinden şifrelenmiş iletişimi sağlayan bir IPSec/IKE VPN bağlantısıdır. siteden siteye bağlantı hello gecikme Hello trafiğin hello Internet geçeceğini öngörülemeyen, taşımaktadır.
- **Azure ExpressRoute:** ağınız ve Azure arasında bir expressroute bağlantı ortağı ile oluşturulmuş. Bu bağlantı özeldir. Trafik hello Internet erişmez. ExpressRoute bağlantısı için hello gecikme süresini tahmin edilebilir, olduğu hello Internet trafiği çapraz geçiş değil.

Merhaba okuma tüm hello önceki bağlantı seçenekleri hakkında daha fazla toolearn [bağlantı topoloji diyagramları](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams) makalesi.

## <a name="filtering"></a>Ağ trafiği filtreleme
Ağ trafiği veya her ikisini seçenekleri aşağıdaki hello kullanarak alt ağlar arasında filtreleyebilirsiniz:
- **Ağ güvenlik grubu (NSG):** her NSG, kaynak ve hedef IP adresi, bağlantı noktası ve protokol toofilter trafiğini etkinleştiren birden fazla gelen ve giden güvenlik kuralları içerebilir. Bir NSG tooeach bir VM'de NIC uygulayabilirsiniz. Bir NSG toohello alt bir NIC de uygulayabilir veya diğer Azure kaynak bağlı. Merhaba okuma Nsg'ler hakkında daha fazla toolearn [ağ güvenlik grupları](virtual-networks-nsg.md) makalesi.
- **Ağ sanal Gereçleri (NVA):** bir NVA olan bir güvenlik duvarı gibi bir ağ işlevi gerçekleştiren yazılımı çalıştıran bir VM. Hello kullanılabilir NVAs listesini görüntülemek [Azure Marketi](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). NVAs WAN iyileştirmesi ve diğer ağ trafiği işlevleri sağlayan de kullanılabilir durumdadır. NVAs, kullanıcı tanımlı ile genellikle kullanılır ya da BGP yolları. Sanal ağlar arasında bir NVA toofilter trafiği de kullanabilirsiniz.

## <a name="routing"></a>Ağ trafiği yönlendirme

Azure kaynakları bağlı tooany alt ağda birbiriyle, varsayılan olarak tüm VNet toocommunicate etkinleştirmek yönlendirme tabloları oluşturur. Ya da uygulayabilir veya seçenekleri toooverride aşağıdaki hello her ikisi de Azure oluşturduğu varsayılan yolların hello:
- **Kullanıcı tanımlı yollar:** özel yol tablolarını her alt ağ trafiği yönlendirilmiş toofor olduğu denetleyen yollar oluşturabilirsiniz. Merhaba okuyun, kullanıcı tanımlı yollar hakkında daha fazla toolearn [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md) makalesi.
- **BGP yolları:** bir Azure VPN ağ geçidi veya ExpressRoute bağlantısı kullanarak VNet tooyour şirket içi ağınıza bağlanıyorsanız, BGP yolları tooyour sanal ağlar yayabilirsiniz.

## <a name="pricing"></a>Fiyatlandırma

Güvenlik grupları sanal ağlar, alt ağlar, yol tablolarını veya ağ için ücret ödemeden yoktur. Giden Internet bant genişliği kullanımı, ortak IP adresleri, sanal ağ eşlemesi, VPN ağ geçitleri ve ExpressRoute her kendi fiyatlandırma yapılarına sahip. Görünüm hello [sanal ağ](https://azure.microsoft.com/pricing/details/virtual-network), [VPN ağ geçidi](https://azure.microsoft.com/pricing/details/vpn-gateway), ve [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) sayfalar daha fazla bilgi için fiyatlandırma.

## <a name="faq"></a>SSS

Sanal ağ hakkında sık sorulan sorular tooreview bkz hello [Virtual Network SSS](virtual-networks-faq.md) makalesi.


## <a name="next-steps"></a>Sonraki adımlar

- İlk sanal ağınızı oluşturmak ve hello hello adımları tamamlayarak birkaç VM'ler tooit bağlanmak [ilk sanal ağınızı oluşturmak](virtual-network-get-started-vnet-subnet.md) makalesi.
- Merhaba hello adımları tamamlayarak bir noktadan siteye bağlantı tooa VNet oluşturma [noktadan siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.
- Merhaba bazıları hakkında bilgi edinin başka bir anahtar [ağ yeteneklerini](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure.
