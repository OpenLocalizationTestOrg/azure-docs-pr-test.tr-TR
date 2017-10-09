---
title: "Altyapı yönergeleri - Linux ağ aaaAzure | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde sanal ağı dağıtmak için hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
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
ms.openlocfilehash: f3f49b135b1f9bca3fd463e9ff27299fb97908c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a>Azure altyapı yönergeleri Linux VM'ler için ağ oluşturma

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Bu makalede, planlama adımları Azure içindeki sanal ağ ve bağlantı için mevcut şirket içi ortamlar arasında gerekli anlama hello odaklanır.

## <a name="implementation-guidelines-for-virtual-networks"></a>Sanal ağlar için uygulama rehberi
Kararları:

* Ne tür sanal ağı toohost BT iş yükü veya altyapı zorunda (yalnızca Bulut veya şirket içi)?
* Şirket içi sanal ağlar için ne kadar adres alanı, toohost hello alt ağları ve sanal makineleri şimdi ve makul genişletme hello içinde gelecekteki gerekiyor mu?
* Siz toocreate giden sanal ağlar merkezi veya her kaynak grubu için tek tek sanal ağlar oluşturmanız misiniz?

Görevler:

* Oluşturulan hello sanal ağlar toobe Hello adres alanı tanımlayın.
* Alt ağları ve hello adres alanı her Hello kümesi tanımlayın.
* Şirket içi sanal ağlar için yerel ağ adres alanları VM'ler hello sanal ağ gereksinimi tooreach hello hello şirket içi konumların hello kümesini tanımlar.
* Şirket içi ağ takım tooensure hello uygun yönlendirme oluştururken yapılandırılmış çalışmak sanal ağlar arası.
* Adlandırma kuralınızın kullanarak hello sanal ağ oluşturun.

## <a name="virtual-networks"></a>Sanal ağlar
Sanal makineler (VM'ler) arasındaki gerekli toosupport iletişim sanal ağlardır. Fiziksel ağlarda olduğu gibi ile yük dengeleme ve alt ağlar, özel IP adresi, DNS ayarlarını, güvenlik filtresini tanımlayın. Kullanarak bir [VPN ağ geçidi](../../vpn-gateway/vpn-gateway-about-vpngateways.md) veya [hızlı rota devresi](../../expressroute/expressroute-introduction.md), Azure sanal ağlar tooyour şirket içi ağlara bağlanın. Daha fazla bilgi edinebilirsiniz [sanal ağlar ve bileşenleri](../../virtual-network/virtual-networks-overview.md).

Kaynak gruplarını kullanarak, sanal ağ bileşenlerinizin nasıl tasarlayacağınızı esneklik bulunur. Sanal makineleri, kendi kaynak grubu dışında toovirtual ağlar bağlanabilir. Ortak tasarım yaklaşımı ortak ekibi tarafından yönetilebilir, Çekirdek Ağ altyapınızın içeren merkezi toocreate kaynak grupları olacaktır. VM'ler ve uygulamalarını tooseparate kaynak grupları dağıtıldı. Bu yaklaşım uygulama sahipleri erişime hello daha geniş sanal ağ kaynaklarına erişim toohello yapılandırması açmadan Vm'leri içeren toohello kaynak grubu.

## <a name="site-connectivity"></a>Site bağlantısı
### <a name="cloud-only-virtual-networks"></a>Yalnızca bulut sanal ağlar
Şirket içi kullanıcıları ve bilgisayarları bir Azure sanal ağında devam eden bağlantı tooVMs gerektirmez, sanal ağ tasarımınızı düz İleri şöyledir:

![Temel yalnızca bulut sanal ağ diyagramı](./media/infrastructure-networking-guidelines/vnet01.png)

Bu genellikle bir Internet tabanlı bir web sunucusu gibi Internet'e yönelik iş yükleri için yaklaşımdır. SSH veya noktadan siteye VPN bağlantıları kullanarak bu sanal makineleri yönetebilirsiniz.

Tooyour şirket içi ağ bağlanmayan olduğundan, yalnızca Azure sanal ağlar herhangi bir kısmının hello özel IP adres alanı kullanabilirsiniz. Merhaba adres alanı hello olabilir, aynı özel alan şirket içi kullanın.

### <a name="cross-premises-virtual-networks"></a>Şirket içi sanal ağlar
Şirket içi kullanıcıları ve bilgisayarları bir Azure sanal ağında devam eden bağlantı tooVMs gerekiyorsa, bir şirket içi sanal ağ oluşturun. Merhaba sanal ağ tooyour şirket içi ağ ExpressRoute veya siteden siteye VPN bağlantısı ile bağlanır.

![Şirket içi sanal ağ diyagramı](./media/infrastructure-networking-guidelines/vnet02.png)

Bu yapılandırmada, hello Azure sanal ağı aslında bir bulut tabanlı ve Şirket ağınızın uzantısıdır.

Bağlandıklarında tooyour şirket içi ağ için şirket içi sanal ağlar benzersiz olduğundan, kuruluşunuz tarafından kullanılan hello adres alanı bir kısmı kullanmanız gerekir. Merhaba aynı şekilde farklı Bu Kurumsal konumların belirli bir IP alt ağı atanır, ağınızı genişletirsiniz Azure başka bir konum haline gelir.

tooallow paketleri tootravel şirket içi sanal ağ tooyour şirket içi ağınızdan hello sanal ağ için hello yerel ağ tanımının bir parçası olarak ilgili şirket içi adres öneklerini hello kümesi yapılandırmanız gerekir. Bağlı olarak Hello adres alanı kümesinin hello sanal ağ ve hello ilgili şirket içi konumlara, hello yerel ağda birçok adres öneklerini olabilir.

Bir yalnızca bulut sanal ağ tooa şirket içi sanal ağ dönüştürebilir, ancak büyük olasılıkla toore IP Azure kaynaklarına ve sanal ağ adres alanı gerektirir. Bu nedenle, bir IP alt ağı atadığınızda, sanal ağ toobe bağlı tooyour şirket içi ağ gerekip gerekmediğini dikkatlice düşünün.

## <a name="subnets"></a>Alt ağlar
Alt ağlar da izin verir, ya da mantıksal olarak ilişkili tooorganize kaynakları (örneğin, toohello VM'ler için bir alt ağ ile ilişkilendirilmiş aynı uygulama), ya da fiziksel olarak (örneğin, her kaynak grubu bir alt ağ). Alt ağ yalıtım teknikleri ek güvenlik için de kullanabilirsiniz.

Şirket içi sanal ağlar için hello sahip alt ağlara tasarlamanız gerekir şirket içi kaynakları için kullandığınız aynı kuralları. **Azure kullandığı her alt ağ için hello adres alanının ilk üç IP adreslerini her zaman hello**. toodetermine hello numarası hello alt ağ için gereken adresler artık ihtiyacınız VM hello sayısı sayım tarafından başlar. Gelecekteki büyümeyi de tahmin etmek ve tablo toodetermine hello hello alt ağ boyutunu aşağıdaki hello kullanın.

| Gerekli VM sayısı | Gerekli konak bit sayısı | Merhaba alt ağ boyutu |
| --- | --- | --- |
| 1–3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> Normal şirket içi alt ağlar için başlangıç adresi sayısı üst sınırı konak n konak BITS ile bir alt ağ için 2.<sup> n </sup> – 2. Azure alt ağ için ana bilgisayar adresleri bir alt n konak BITS ile hello sayısı 2 sayısıdır<sup> n </sup> – 5 (2 ve 3 Azure her alt ağda kullanan hello adresler için).
> 
> 

Çok küçük bir alt ağ boyutu seçerseniz, toore IP ve hello VM'ler hello alt yeniden dağıtın.

## <a name="network-security-groups"></a>Ağ Güvenlik Grupları
Ağ güvenlik grupları kullanılarak sanal ağlarınız arasında akan filtreleme kuralları toohello trafik uygulayabilirsiniz. Bağlantı noktaları, vb. izin verilen gelen ve giden trafik, kaynak ve hedef IP aralıkları, denetleme, sanal ağ ortamınızın ayrıntılı filtreleme kuralları toosecure oluşturabilirsiniz. Ağ güvenlik grupları, bir sanal ağ veya doğrudan sanal ağ arabirimi verilen tooa içinde uygulanan toosubnets olabilir. Bu ağ güvenlik grubu, sanal ağlar üzerindeki trafik filtreleme belirli bir düzeyde toohave önerilir. Daha fazla bilgi edinebilirsiniz [ağ güvenlik grupları](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Ek ağ bileşenleri
Şirket içi fiziksel ağ altyapısına gibi Azure sanal ağı daha fazlasını alt ağları ve IP adresleme içerebilir. Uygulama altyapınızı tasarlarken, tooincorporate isteyebilirsiniz bu ek bileşenleri bazıları:

* [VPN ağ geçitleri](../../vpn-gateway/vpn-gateway-about-vpngateways.md) -bağlanmak Azure sanal ağlar tooother Azure sanal ağları veya siteden siteye VPN bağlantısı üzerinden tooon içi ağlara bağlanın. Hızlı rota bağlantıları ayrılmış, güvenli bağlantılar için uygulayın. Bu gibi durumlarda, kullanıcıları doğrudan erişim de noktadan siteye VPN bağlantıları ile sağlayabilirsiniz.
* [Yük Dengeleyici](../../load-balancer/load-balancer-overview.md) -trafik istediğiniz gibi iç ve dış trafiği için Yük Dengeleme sağlar.
* [Uygulama ağ geçidi](../../application-gateway/application-gateway-introduction.md) - hello uygulama katmanında Yük Dengeleme, web uygulamaları için bazı ek avantajları sağlayan yerine hello Azure yük dengeleyici dağıtımı HTTP.
* [Trafik Yöneticisi](../../traffic-manager/traffic-manager-overview.md) - DNS tabanlı uygulamanız farklı bölgelerdeki Azure veri merkezlerinde dışında dağıtım toodirect son kullanıcılar toohello yakın kullanılabilir uygulama uç noktası, izin verme, toohost trafiği.

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

