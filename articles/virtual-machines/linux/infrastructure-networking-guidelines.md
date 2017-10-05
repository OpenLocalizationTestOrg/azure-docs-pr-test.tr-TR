---
title: "Azure altyapı yönergeleri - Linux ağ | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde sanal ağı dağıtmak için anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7ebd5da-3c62-45e8-ad90-6c73a37ebeb1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 13e041956c05bec522c83587f8a7f99ac1ceb510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a>Azure altyapı yönergeleri Linux VM'ler için ağ oluşturma

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Bu makalede, mevcut şirket içi ortamlar arasında Azure içindeki sanal ağ ve bağlantı için gerekli olan planlama adımları anlamaya odaklanır.

## <a name="implementation-guidelines-for-virtual-networks"></a>Sanal ağlar için uygulama rehberi
Kararları:

* BT iş yükü veya altyapı barındırmak gereken ne tür bir sanal ağ (yalnızca Bulut veya şirket içi)?
* Şirket içi sanal ağlar için ne kadar adres alanı, şimdi ve gelecekte makul genişletme için alt ağları ve sanal makineleri barındırmak gerekiyor mu?
* Merkezi Sanal ağları veya her kaynak grubu için tek tek sanal ağlar oluşturmak için yapacaksınız?

Görevler:

* Oluşturulacak sanal ağlar için kullanılan adres alanını tanımlayın.
* Her alt ağları ve adres alanı kümesini tanımlar.
* Şirket içi sanal ağlar için sanal ağ içindeki VM'ler ulaşması gereken şirket içi konumları için yerel ağ adres alanları kümesini tanımlar.
* İş oluşturma sanal ağlar arası ile şirket içi uygun yönlendirme emin olmak için ağ takım yapılandırılır.
* Adlandırma kuralınızın kullanarak sanal ağ oluşturun.

## <a name="virtual-networks"></a>Sanal ağlar
Sanal ağlar, sanal makineleri (VM'ler) arasındaki iletişimi desteklemek gereklidir. Fiziksel ağlarda olduğu gibi ile yük dengeleme ve alt ağlar, özel IP adresi, DNS ayarlarını, güvenlik filtresini tanımlayın. Kullanarak bir [VPN ağ geçidi](../../vpn-gateway/vpn-gateway-about-vpngateways.md) veya [hızlı rota devresi](../../expressroute/expressroute-introduction.md), Azure sanal ağı şirket içi ağlarınız bağlanabilir. Daha fazla bilgi edinebilirsiniz [sanal ağlar ve bileşenleri](../../virtual-network/virtual-networks-overview.md).

Kaynak gruplarını kullanarak, sanal ağ bileşenlerinizin nasıl tasarlayacağınızı esneklik bulunur. Sanal makineleri, kendi kaynak grubu dışında sanal ağlara bağlanabilir. Ortak tasarım yaklaşımı ortak ekibi tarafından yönetilebilir, Çekirdek Ağ altyapınızın içeren merkezi kaynak grupları oluşturmak için olacaktır. VM'ler ve uygulamalarını ayrı kaynak gruplarına dağıtılır. Bu yaklaşım, daha geniş sanal ağ kaynaklarını yapılandırma erişimi açmaya gerek kalmadan Vm'leri içeren kaynak grubu için uygulama sahipleri erişim sağlar.

## <a name="site-connectivity"></a>Site bağlantısı
### <a name="cloud-only-virtual-networks"></a>Yalnızca bulut sanal ağlar
Şirket içi kullanıcıları ve bilgisayarları bir Azure sanal ağındaki VM'ler için devam eden bağlantısı gerekiyor mu, sanal ağ tasarımınızı düz İleri şöyledir:

![Temel yalnızca bulut sanal ağ diyagramı](./media/infrastructure-networking-guidelines/vnet01.png)

Bu genellikle bir Internet tabanlı bir web sunucusu gibi Internet'e yönelik iş yükleri için yaklaşımdır. SSH veya noktadan siteye VPN bağlantıları kullanarak bu sanal makineleri yönetebilirsiniz.

Şirket içi ağınıza bağlanmayan olduğundan, yalnızca Azure sanal ağlar özel IP adres alanı herhangi bir kısmının kullanabilirsiniz. Adres alanı kullanımı şirket içi aynı özel alanı olabilir.

### <a name="cross-premises-virtual-networks"></a>Şirket içi sanal ağlar
Şirket içi kullanıcıları ve bilgisayarları bir Azure sanal ağındaki VM'ler için devam eden bağlantı gerekiyorsa, bir şirket içi sanal ağ oluşturun. Sanal ağ, bir ExpressRoute veya siteden siteye VPN bağlantısı ile şirket içi ağınıza bağlayın.

![Şirket içi sanal ağ diyagramı](./media/infrastructure-networking-guidelines/vnet02.png)

Bu yapılandırmada, Azure sanal ağı aslında bir bulut tabanlı ve Şirket ağınızın uzantısıdır.

Şirket içi ağınıza bağlanmak için sanal ağlar benzersiz olduğundan, kuruluşunuz tarafından kullanılan adres alanının bir bölümü kullanmalısınız şirketler arası. Ağınızı genişletirsiniz farklı Kurumsal konumların belirli bir IP alt ağı atanan aynı şekilde, Azure başka bir konum haline gelir.

Şirket içi sanal ağdan şirket içi ağınıza paketlerin izin vermek için sanal ağ yerel ağ tanımının bir parçası olarak ilgili şirket içi adres öneklerini kümesi yapılandırmanız gerekir. Sanal ağın adres alanı ve uygun şirket içi konumlara kümesi bağlı olarak, yerel ağ birçok adres öneklerini olabilir.

Bir şirket içi sanal ağa bir yalnızca bulut sanal ağ dönüştürebilirsiniz, ancak büyük olasılıkla yeniden-IP Azure kaynaklarına ve sanal ağ adres alanı gerekir. Bu nedenle, bir sanal ağı bir IP alt ağı atadığınızda, şirket içi ağınıza bağlı olması gerekip gerekmediğini dikkatlice düşünün.

## <a name="subnets"></a>Alt ağlar
Alt ağlar izin ilgili kaynakları düzenleyin ya da mantıksal olarak (örneğin, aynı uygulamanın ilişkili VM'ler için bir alt ağ), ya da fiziksel olarak (örneğin, her kaynak grubu bir alt ağ). Alt ağ yalıtım teknikleri ek güvenlik için de kullanabilirsiniz.

Şirket içi sanal ağlar için şirket içi kaynakları için kullandığınız aynı kurallarına sahip alt ağlara tasarlamanız gerekir. **Azure her alt ağ için her zaman ilk üç adres alanı IP adreslerini kullanan**. Alt ağ için gereken adresi sayısını belirlemek için artık ihtiyacınız VM'ler sayım tarafından başlatın. Gelecekteki büyümeyi de tahmin etmek ve alt ağ boyutunu belirlemek için aşağıdaki tabloyu kullanın.

| Gerekli VM sayısı | Gerekli konak bit sayısı | Alt ağ boyutu |
| --- | --- | --- |
| 1–3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> Normal şirket içi alt ağlar için n konak BITS ile bir alt ağ için ana bilgisayar adresi sayısı üst sınırı 2.<sup> n </sup> – 2. Azure alt ağı için bir alt n konak BITS ile ana bilgisayar adresi sayısı üst sınırı 2'dir<sup> n </sup> – 5 (2 ve 3 Azure her alt ağda kullanan adresler için).
> 
> 

Çok küçük bir alt ağ boyutu seçerseniz, yeniden-IP ve alt ağ içindeki VM'ler yeniden dağıtın.

## <a name="network-security-groups"></a>Ağ Güvenlik Grupları
Ağ güvenlik grupları kullanılarak sanal ağlarınız arasında akan trafik filtreleme kurallarını uygulayabilirsiniz. Bağlantı noktaları, vb. izin verilen gelen ve giden trafik, kaynak ve hedef IP aralıkları, denetleme sanal ağ ortamınızın güvenliğini sağlamak için ayrıntılı filtreleme kuralları oluşturabilirsiniz. Bir sanal ağ içindeki alt ağlara veya doğrudan verilen sanal ağ arabirimi için ağ güvenlik grupları uygulanabilir. Ağ güvenlik grubu, sanal ağlar üzerindeki trafik filtreleme belirli bir düzeyde olması önerilir. Daha fazla bilgi edinebilirsiniz [ağ güvenlik grupları](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Ek ağ bileşenleri
Şirket içi fiziksel ağ altyapısına gibi Azure sanal ağı daha fazlasını alt ağları ve IP adresleme içerebilir. Uygulama altyapınızı tasarlarken, bu ek bileşenleri bazıları dahil isteyebilirsiniz:

* [VPN ağ geçitleri](../../vpn-gateway/vpn-gateway-about-vpngateways.md) - Azure sanal ağlar Azure diğer sanal ağlara bağlanmak veya siteden siteye VPN bağlantısı üzerinden şirket içi ağlara bağlanın. Hızlı rota bağlantıları ayrılmış, güvenli bağlantılar için uygulayın. Bu gibi durumlarda, kullanıcıları doğrudan erişim de noktadan siteye VPN bağlantıları ile sağlayabilirsiniz.
* [Yük Dengeleyici](../../load-balancer/load-balancer-overview.md) -trafik istediğiniz gibi iç ve dış trafiği için Yük Dengeleme sağlar.
* [Uygulama ağ geçidi](../../application-gateway/application-gateway-introduction.md) - uygulama katmanında Yük Dengeleme, web uygulamaları için bazı ek avantajları sağlayan yerine Azure yük dengeleyici dağıtımı HTTP.
* [Trafik Yöneticisi](../../traffic-manager/traffic-manager-overview.md) - DNS tabanlı trafiği doğrudan son kullanıcılara farklı bölgelerdeki Azure veri merkezlerinde dışında uygulamanızı barındırmak sağlayarak en yakın kullanılabilir uygulama uç noktası, dağıtım.

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

