---
title: "Sanal ağ (VNet) aaaAzure Plan ve Tasarım Kılavuzu | Microsoft Docs"
description: "Azure sanal ağları tooplan ve tasarım nasıl yalıtımı, bağlantı ve konum gereksinimlerinizi temel alarak öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Planlama ve Azure sanal ağlar tasarlama
VNet tooexperiment ile oluşturma yeterince kolay, ancak büyük olasılıkla, zaman toosupport hello üretim, kuruluşunuzun gereksinimlerini birden çok sanal ağlar dağıtır. Bazı planlama ve tasarım ile mümkün toodeploy sanal ağlar olabilir ve daha etkili bir şekilde ihtiyacınız hello kaynakları bağlanın. Sanal ağlar ile bilmiyorsanız, önermiştir, [sanal ağlar hakkında bilgi edinin](virtual-networks-overview.md) ve [nasıl toodeploy](virtual-networks-create-vnet-arm-pportal.md) devam etmeden önce bir.

## <a name="plan"></a>Planlama
Azure Abonelikleri, bölgeler ve ağ kaynaklarının kapsamlı olarak anlamayı başarısı için önemlidir. Bir başlangıç noktası olarak dikkat edilecek noktalar hello listesini kullanabilirsiniz. Bu konuları anladığınızda, ağ tasarımınız için hello gereksinimleri tanımlayabilirsiniz.

### <a name="considerations"></a>Dikkat edilmesi gerekenler
Aşağıdaki sorular planlama hello yanıtlamadan önce hello aşağıdakileri dikkate alın:

* Her şeyi Azure içinde oluşturduğunuz bir veya daha fazla kaynak oluşur. Bir sanal makine (VM) bir kaynak, bir VM tarafından kullanılan hello ağ bağdaştırıcısı (NIC) bir kaynak arabirimidir, bir NIC tarafından kullanılan hello genel IP adresini bir kaynaktır, hello VNet hello NIC bağlı toois kaynak.
* Kaynakları içinde oluşturduğunuz bir [Azure bölgesi](https://azure.microsoft.com/regions/#services) ve abonelik. Kaynaklar yalnızca aynı bölge ve abonelik hello kaynak bulunduğu hello mevcut bağlı tooa sanal ağ olabilir.
* Sanal ağlar tooeach diğer kullanarak bağlanabilir:
    * **[Sanal Ağ eşlemesi](virtual-network-peering-overview.md)**: hello sanal ağlar hello aynı bulunmalıdır Azure bölgesi. Eşlenen sanal ağlarda bulunan kaynaklar arasındaki bant genişliği olan hello aynı hello kaynaklara bağlı toohello değilmiş gibi aynı sanal ağ.
    * **Bir Azure [VPN ağ geçidi](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: hello sanal ağlar hello aynı bulunabilir veya farklı Azure bölgeleri. Bir VPN ağ geçidi üzerinden bağlı sanal ağlarda bulunan kaynaklar arasındaki bant genişliği hello VPN ağ geçidi hello bant genişliği ile sınırlıdır.
* Merhaba birini kullanarak sanal ağlar tooyour şirket ağına bağlanabilecek [bağlantı seçenekleri](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) Azure içinde kullanılabilir.
* Farklı kaynaklar gruplandırılabilir birlikte [kaynak grupları](../azure-resource-manager/resource-group-overview.md#resource-groups), bir birim olarak daha kolay toomanage hello kaynak yapma. Merhaba kaynakların toohello ait olduğu sürece bir kaynak grubu birden çok bölgelerdeki kaynakları içerebilir aynı abonelik.

### <a name="define-requirements"></a>Gereksinimleri tanımlayın
Aşağıda Hello soruları Azure ağ tasarımınız için başlangıç noktası olarak kullanın.    

1. Azure konumları, ne olur toohost sanal ağlar kullanmak?
2. Bu Azure konumları arasında tooprovide iletişim gerekiyor mu?
3. Azure VNet(s) ve şirket içi inizdeki arasında tooprovide iletişimi gerekiyor mu?
4. Bir hizmet (Iaas) sanal olarak kaç altyapı bulut rolleri ve web uygulamaları çözümünüz için gereken hizmetleri?
5. Sanal makineleri (yani ön uç web sunucuları ve arka uç veritabanı sunucuları) gruplarını temel alan tooisolate trafiği gerekiyor mu?
6. Sanal gereçler kullanma toocontrol trafik akışı gerekiyor mu?
7. Kullanıcılar gerek farklı kümelerini izinleri toodifferent Azure kaynaklarını musunuz?

### <a name="understand-vnet-and-subnet-properties"></a>VNet ve alt ağ özelliklerini anlama
VNet ve alt kaynakları Azure'da çalışan iş yükleri için güvenlik sınırı tanımlamaya yardımcı olacak. Bir sanal ağ adres alanları, CIDR bloğu tanımlı bir koleksiyon tarafından belirlenir.

> [!NOTE]
> Ağ yöneticileri ile CIDR gösteriminde biliyorsunuzdur. CIDR ile bilmiyorsanız [hakkında daha fazla bilgi](http://whatismyipaddress.com/cidr).
>
>

Sanal ağlar, aşağıdaki özelliklere hello içerir.

| Özellik | Açıklama | Kısıtlamalar |
| --- | --- | --- |
| **adı** |VNet adı |Yukarı too80 karakter dizisi. Harf, rakam, alt çizgi, nokta veya kısa çizgi içerebilir. Bir harf veya sayı ile başlamalıdır. Bir harf, sayı veya alt çizgi ile bitmelidir. Üst veya küçük harf içerir. |
| **konum** |Azure konumu (Ayrıca başvurulan tooas bölge). |Merhaba geçerli Azure konumlar biri olmalıdır. |
| **addressSpace** |CIDR gösteriminde hello VNet oluşturan adres öneklerini koleksiyonu. |Genel IP adresi aralıklarının da dahil olmak üzere, geçerli CIDR adres bloklarını bir dizi olmalıdır. |
| **alt ağlar** |VNet hello yapmak alt koleksiyonu |Merhaba alt ağ özelliklerini tabloya bakın. |
| **dhcpOptions** |Adlı tek gerekli bir özellik içeren nesne **dnsServers**. | |
| **dnsServers** |VNet hello tarafından kullanılan DNS sunucuları dizisi. Hiçbir sunucu belirtilirse, Azure dahili ad çözümlemesi kullanılır. |Bir dizi yedekleme IP adresine göre too10 DNS sunucuları olması gerekir. |

Bir alt ağ alt bir vnet'in kaynaktır ve adres alanları IP adresi öneklerini kullanarak bir CIDR bloğu içinde kesimleri yardımcı tanımlayın. NIC toosubnets ve çeşitli iş yükleri için bağlantı sağlama bağlı tooVMs eklenebilir.

Alt ağları aşağıdaki özelliklere hello içerir.

| Özellik | Açıklama | Kısıtlamalar |
| --- | --- | --- |
| **adı** |Alt ağ adı |Yukarı too80 karakter dizisi. Harf, rakam, alt çizgi, nokta veya kısa çizgi içerebilir. Bir harf veya sayı ile başlamalıdır. Bir harf, sayı veya alt çizgi ile bitmelidir. Üst veya küçük harf içerir. |
| **konum** |Azure konumu (Ayrıca başvurulan tooas bölge). |Merhaba geçerli Azure konumlar biri olmalıdır. |
| **addressPrefix** |Merhaba alt ağ CIDR gösteriminde oluşturan tek adresi öneki |Merhaba sanal ağınızın adres alanlarından birini parçası olan tek bir CIDR bloğu olmalıdır. |
| **networkSecurityGroup** |NSG uygulanır toohello alt ağ | |
| **routeTable** |Yol tablosu toohello alt uygulanan | |
| **Ipconfigurations** |NIC bağlı toohello alt ağı tarafından kullanılan IP yapılandırması nesneleri koleksiyonu | |

### <a name="name-resolution"></a>Ad çözümlemesi
Varsayılan olarak, sanal ağınızı kullanır [Azure tarafından sağlanan ad çözümlemesi](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve adlarını hello VNet içinde veya üzerinde genel Internet hello. Ancak, sanal ağlar tooyour şirket içi veri merkezleri bağlanıyorsanız, tooprovide gerekir [kendi DNS sunucusu](virtual-networks-name-resolution-for-vms-and-role-instances.md) ağlarınız arasında tooresolve adları.  

### <a name="limits"></a>Sınırlar
Merhaba ağ sınırları Hello gözden [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) tasarımınızı herhangi bir hello sınırları ile çakışan değil makale tooensure. Bazı sınırlar bir destek bileti açılarak artırılabilir.

### <a name="role-based-access-control-rbac"></a>Rol Tabanlı Erişim Denetimi (RBAC)
Kullanabileceğiniz [Azure RBAC](../active-directory/role-based-access-built-in-roles.md) toocontrol hello farklı kullanıcılara erişim düzeyini Azure'da toodifferent kaynaklara sahip olabilir. Bu şekilde hello iş gereksinimlerine göre ekibiniz tarafından yapılan ayırabilirsiniz.

Sanal ağlar olarak uzak kaygı hello kullanıcılar **ağ Katılımcısı** rol Azure Resource Manager sanal ağ kaynaklarına üzerinde tam denetime sahiptir. Benzer şekilde, hello kullanıcılar **Klasik ağ Katılımcısı** rol Klasik sanal ağ kaynaklarına üzerinde tam denetime sahiptir.

> [!NOTE]
> Ayrıca [kendi rolleri oluşturma](../active-directory/role-based-access-control-configure.md) tooseparate yönetim gereksinimlerinizi.
>
>

## <a name="design"></a>Tasarlayın
Merhaba toohello sorulara hello yanıtlar öğrendikten sonra [planlama](#Plan) bölümünde, önce sanal ağlar tanımlama hello aşağıdakileri gözden geçirin.

### <a name="number-of-subscriptions-and-vnets"></a>Abonelikler ve sanal ağlar sayısı
Birden çok sanal ağlar senaryoları aşağıdaki hello oluşturmayı düşünebilirsiniz:

* **Azure farklı konumlarda yerleştirilen toobe gereken sanal makineleri**. Azure sanal ağları bölgesel. Bunlar konumları yayılamaz. Bu nedenle toohost VM'ler istediğiniz her Azure konumu için en az bir VNet gerekir.
* **Birbirinden tamamen yalıtılmış toobe gerektiren iş yüklerini**. Aynı IP adresi alanları, tooisolate farklı iş yükleri birbirinden ayrı Vnet'ler, o bile kullanım hello oluşturabilirsiniz.

Yukarıda gördüğünüz hello her bölge, abonelik başına kısıtlamalardır aklınızda bulundurun. Azure'da koruyabilirsiniz kaynakların birden çok abonelik tooincrease hello sınırı kullanabileceğiniz anlamına gelir. Siteden siteye VPN ya da farklı Aboneliklerde tooconnect sanal ağlar bir expressroute bağlantı hattı kullanabilirsiniz.

### <a name="subscription-and-vnet-design-patterns"></a>Abonelik ve VNet tasarım desenleri
Merhaba tabloda abonelikleri ve sanal ağlar kullanmak için bazı ortak tasarım desenleri gösterir.

| Senaryo | Diyagram | Uzmanları | Simgeler |
| --- | --- | --- | --- |
| Tek bir abonelik, uygulama başına iki sanal ağlar |![Tek bir abonelik](./media/virtual-network-vnet-plan-design-arm/figure1.png) |Yalnızca bir abonelik toomanage. |Sanal ağlar maksimum sayısı her Azure bölgesi. Daha fazla abonelik bundan sonra gerekir. Gözden geçirme hello [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) Ayrıntılar için makale. |
| Uygulama, uygulama başına iki Vnet başına tek abonelikle |![Tek bir abonelik](./media/virtual-network-vnet-plan-design-arm/figure2.png) |Abonelik başına yalnızca iki Vnet kullanır. |Çok fazla uygulama olduğunda daha zor toomanage. |
| Departman, uygulama başına iki Vnet başına tek abonelikle. |![Tek bir abonelik](./media/virtual-network-vnet-plan-design-arm/figure3.png) |Abonelik sayısı ve sanal ağlar arasında dengeleyin. |Sanal ağlar maksimum sayısı her iş birimi (abonelik). Gözden geçirme hello [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) Ayrıntılar için makale. |
| Departman, uygulama grubu başına iki Vnet başına tek abonelikle. |![Tek bir abonelik](./media/virtual-network-vnet-plan-design-arm/figure4.png) |Abonelik sayısı ve sanal ağlar arasında dengeleyin. |Alt ağları ve Nsg'ler kullanarak uygulamaları yalıtılmış gerekir. |

### <a name="number-of-subnets"></a>Alt ağların sayısı
Sanal ağ senaryoları aşağıdaki hello içinde birden çok alt ağların dikkate almanız gerekir:

* **Bir alt ağdaki tüm NIC'ler için yeterli özel IP adresleri**. Alt ağ adresi alanınızı hello sayısında NIC'ler hello alt ağ için yeterli IP adresine içermiyorsa, birden çok alt ağı toocreate gerekir. Azure kullanılamaz her alt ağdan 5 özel IP adresleri ayırır göz önünde bulundurun: ilk hello ve son adreslerini hello adres alanı (Merhaba alt ağ adresi ve çok noktaya yayın) ve 3 adresleri toobe dahili olarak (DHCP ve DNS amaçlar için) kullanılır.
* **Güvenlik**. Yapı ve farklı uygulamak çok katmanlı olan iş yükleri için birbirinden VM'lerin alt ağları tooseparate gruplarını kullanabilirsiniz [güvenlik gruplarını (Nsg'ler) ağ](virtual-networks-nsg.md#subnets) bu alt ağlardan için.
* **Karma bağlantı**. VPN ağ geçitleri ve ExpressRoute bağlantı hatları çok kullanabilirsiniz[bağlanmak](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) , sanal ağlar tooone başka bir, ve tooyour şirket içi veri center(s). VPN ağ geçitleri ve ExpressRoute bağlantı hatları oluşturulan kendi toobe alt gerektirir.
* **Sanal gereçler**. Güvenlik Duvarı, WAN Hızlandırıcı veya VPN ağ geçidi gibi bir sanal gereç bir Azure VNet kullanabilirsiniz. Bunu yaptığınızda, çok ihtiyacınız[trafiği yönlendirmek](virtual-networks-udr-overview.md) toothose cihazları ve kendi alt ağda yalıtır.

### <a name="subnet-and-nsg-design-patterns"></a>Alt ağı ve NSG tasarım desenleri
Merhaba tabloda alt ağları kullanarak bazı ortak tasarım desenleri gösterir.

| Senaryo | Diyagram | Uzmanları | Simgeler |
| --- | --- | --- | --- |
| Tek alt ağ, uygulama başına uygulama katmanı başına Nsg'ler |![Tek alt ağ](./media/virtual-network-vnet-plan-design-arm/figure5.png) |Yalnızca bir alt ağ toomanage. |Birden çok Nsg'ler gerekli tooisolate her bir uygulama. |
| Uygulama, uygulama katmanı başına Nsg'ler başına bir alt ağ |![Uygulama başına alt ağ](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Daha az Nsg'ler toomanage. |Birden çok alt ağlar toomanage. |
| Uygulama katmanı, uygulama başına Nsg'ler başına bir alt ağ. |![Katman her alt ağ](./media/virtual-network-vnet-plan-design-arm/figure7.png) |Nsg'ler alt ağların sayısı arasında dengeleyin. |Abonelik başına Nsg'ler maksimum sayısı. Gözden geçirme hello [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) Ayrıntılar için makale. |
| Uygulama, her alt ağ Nsg'ler başına uygulama katmanı başına bir alt ağ |![Alt ağına göre uygulama başına katmanı](./media/virtual-network-vnet-plan-design-arm/figure8.png) |Büyük olasılıkla daha az sayıda Nsg'ler. |Birden çok alt ağlar toomanage. |

## <a name="sample-design"></a>Örnek tasarımı
Bu makalede, hello bilgilerinin tooillustrate hello uygulama senaryo aşağıdaki hello göz önünde bulundurun.

Kuzey Amerika 2 veri merkezlerinde ve iki veri merkezleri Avrupa sahip bir şirket için çalışır. 6 tanımlanan uygulamaları karşılıklı farklı müşteri toomigrate tooAzure bir pilot olarak istediğiniz 2 farklı iş birimleri tarafından korunur. Merhaba temel mimari hello uygulamalar için aşağıdaki gibidir:

* App1 ve App2, App3 ve App4 Ubuntu Linux sunucuları üzerinde barındırılan web uygulamalardır. Her uygulama tooa ayrı bir uygulama sunucusu barındıran RESTful hizmetlerini Linux sunuculara bağlanır. Merhaba RESTful hizmetlerini tooa arka uç MySQL veritabanına bağlanın.
* App5 ve App6 Windows Server 2012 R2 çalıştıran Windows sunucularında barındırılan web uygulamalardır. Her uygulama tooa arka uç SQL Server veritabanına bağlar.
* Tüm uygulamalar, şu anda Kuzey Amerika hello şirketin veri merkezlerinde birinde barındırılır.
* Merhaba şirket içi veri merkezleri hello 10.0.0.0/8 adres alanı kullanın.

Toodesign hello aşağıdaki gereksinimleri karşılayan bir sanal ağ çözümü gerekir:

* Her iş birimi diğer iş birimleri kaynak tüketimini tarafından etkilenmez.
* Sanal ağlar ve alt ağları toomake yönetimini daha kolay hello miktarı en aza indirmeniz gerekir.
* Her iş birimi bir tek test/geliştirme tüm uygulamalar için kullanılan VNet olması gerekir.
* Her uygulama kıtada (Kuzey Amerika ve Avrupa'da) başına 2 farklı Azure veri merkezleri içinde barındırılır.
* Her uygulama birbirinden tamamen ayrı tutulur.
* Her uygulama müşteriler tarafından hello Internet erişilebilir HTTP kullanarak.
* Her bir uygulama kullanıcıların bağlı toohello şirket içi veri merkezleri tarafından şifrelenmiş tüneli kullanılarak erişilebilir.
* Bağlantı tooon içi veri merkezleri, var olan VPN cihazları kullanmanız gerekir.
* Merhaba şirketin ağ grubun hello VNet yapılandırmasını üzerinde tam denetimi olmalıdır.
* Her iş birimi geliştiriciler yalnızca mümkün toodeploy VM'ler tooexisting alt olmalıdır.
* Tüm uygulamaları tooAzure (yükseltme ve shift) olarak geçirilecektir.
* her konum Hello veritabanlarında tooother Azure çoğaltmak konumları günde bir kez.
* Her uygulama 5 ön uç web sunucuları, 2 uygulama sunucuları (gerektiğinde) ve 2 veritabanı sunucuları kullanmanız gerekir.

### <a name="plan"></a>Planlama
Merhaba hello soruyu yanıtlayarak planlama tasarımınızı başlamalıdır [gereksinimlerini tanımlamanıza](#Define-requirements) bölümünde aşağıda gösterildiği gibi.

1. Azure konumları, ne olur toohost sanal ağlar kullanmak?

    2 konumlarda Kuzey Amerika ve Avrupa'da 2 konumları. Bu, mevcut şirket içi veri merkezlerinin hello fiziksel konum temelinde seçmeniz gerekir. Bu şekilde, fiziksel konumları tooAzure bağlantısından daha iyi bir gecikme süresi gerekir.
2. Bu Azure konumları arasında tooprovide iletişim gerekiyor mu?

    Evet. Merhaba veritabanları çoğaltılmış tooall konumları olması gerektiğinden.
3. Azure VNet(s) ve şirket içi veri center(s) arasında tooprovide iletişimi gerekiyor mu?

    Evet. Kullanıcıların bağlı olduğundan toohello şirket içi veri merkezleri mümkün tooaccess hello uygulamalar şifrelenmiş tüneli aracılığıyla olması gerekir.
4. Kaç tane Iaas VM'ler çözümünüz için gerekiyor mu?

    200 Iaas VM'ler. App1 ve App2, App3 ve App4 her 5 web sunucularının her, 2 uygulama sunucularının her ve 2 veritabanı sunucuları gerektirir. Uygulama başına 9 Iaas VM'ler veya 36 Iaas Vm'leri toplam olmasıdır. App5 ve App6 5 web sunucuları ve 2 veritabanı sunucuları gerektirir. Uygulama başına 7 Iaas VM'ler veya 14 Iaas Vm'leri toplam olmasıdır. Bu nedenle, her bir Azure bölgesine tüm uygulamalar için 50 Iaas Vm'leri gerekir. Toouse 4 bölgeler ihtiyacımız olduğundan, 200 Iaas Vm'leri olacaktır.

    Ayrıca, Azure Iaas Vm'leri ve şirket içi ağınız arasında tooprovide DNS sunucularının her sanal ağ veya şirket içi veri merkezleri tooresolve adınızı gerekir.
5. Sanal makineleri (yani ön uç web sunucuları ve arka uç veritabanı sunucuları) gruplarını temel alan tooisolate trafiği gerekiyor mu?

    Evet. Her uygulama birbirinden tamamen yalıtılmış olması gerekir ve her uygulama katmanı da yalıtılmış olması gerekir.
6. Sanal gereçler kullanma toocontrol trafik akışı gerekiyor mu?

    Hayır. Sanal gereçler daha fazla ayrıntılı veri düzlemi günlükleri dahil olmak üzere trafik akışı üzerinde denetim kullanılan tooprovide olabilir.
7. Kullanıcılar gerek farklı kümelerini izinleri toodifferent Azure kaynaklarını musunuz?

    Evet. Geliştiriciler yalnızca mümkün toodeploy olmalıdır sırada hello ağ takım hello sanal ağ ayarları üzerinde tam denetim toopre varolan VM ağlarını gerekir.

### <a name="design"></a>Tasarlayın
Abonelikler, sanal ağlar, alt ağları ve Nsg'ler belirtme hello tasarım izlemelisiniz. Nsg'ler burada ele alınacaktır, ancak, daha fazla bilgi edinmek [Nsg'ler](virtual-networks-nsg.md) tasarımınızı tamamlamadan önce.

**Abonelikler ve sanal ağlar sayısı**

hello gereksinimleri aşağıdaki ilgili toosubscriptions ve sanal ağlar şunlardır:

* Her iş birimi diğer iş birimleri kaynak tüketimini tarafından etkilenmez.
* Sanal ağlar ve alt ağları hello miktarı en aza indirmeniz gerekir.
* Her iş birimi bir tek test/geliştirme tüm uygulamalar için kullanılan VNet olması gerekir.
* Her uygulama kıtada (Kuzey Amerika ve Avrupa'da) başına 2 farklı Azure veri merkezleri içinde barındırılır.

Bu gereksinimlerine bağlı olarak, her iş birimi için bir abonelik gerekiyor. Bu şekilde, bir iş biriminin kaynakları tüketiminin sınırları diğer iş birimleri için sayar değil. Ve toominimize hello Vnet sayısı istediğinden hello kullanmayı düşünmelisiniz **departman, uygulama grubu başına iki Vnet başına tek abonelikle** desen aşağıda görüldüğü gibi.

![Tek bir abonelik](./media/virtual-network-vnet-plan-design-arm/figure9.png)

Ayrıca her bir Vnet'teki toospecify hello adres alanı gerekir. Gereksinim duyduğunuz beri hello arasında bağlantı içi veri merkezleri hello Azure bölgeleri, Azure sanal ağlar için kullanılan hello adres alanı ile Merhaba şirket içi ağ artar olamaz ve her sanal ağ tarafından kullanılan hello adres alanı ile var olan diğer sanal ağlardan artar değil. Bu gereksinimleri hello adres alanları toosatisfy aşağıda hello tablosundaki kullanabilirsiniz.  

| **Abonelik** | **Sanal ağ** | **Azure bölgesi** | **Adres alanı** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |Batı ABD |172.16.0.0/16 |
| BU1 |ProdBU1US2 |Doğu ABD |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |Kuzey Avrupa |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |Batı Avrupa |172.19.0.0/16 |
| BU1 |TestDevBU1 |Batı ABD |172.20.0.0/16 |
| BU2 |TestDevBU2 |Batı ABD |172.21.0.0/16 |
| BU2 |ProdBU2US1 |Batı ABD |172.22.0.0/16 |
| BU2 |ProdBU2US2 |Doğu ABD |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |Kuzey Avrupa |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |Batı Avrupa |172.25.0.0/16 |

**Alt ağları ve Nsg'ler sayısı**

hello gereksinimleri aşağıdaki ilgili toosubnets ve Nsg'ler şunlardır:

* Sanal ağlar ve alt ağları hello miktarı en aza indirmeniz gerekir.
* Her uygulama birbirinden tamamen ayrı tutulur.
* Her uygulama müşteriler tarafından hello Internet erişilebilir HTTP kullanarak.
* Her bir uygulama kullanıcıların bağlı toohello şirket içi veri merkezleri tarafından şifrelenmiş tüneli kullanılarak erişilebilir.
* Bağlantı tooon içi veri merkezleri, var olan VPN cihazları kullanmanız gerekir.
* her konum Hello veritabanlarında tooother Azure çoğaltmak konumları günde bir kez.

Bu gereksinimlerine bağlı olarak, size uygulama katmanı başına bir alt ağ ve uygulama başına Nsg'ler toofilter trafiği kullanın. Bu şekilde, yalnızca 3 alt ağların her bir Vnet'teki (ön uç, uygulama katmanı ve veri katmanı) ve her alt ağ uygulaması başına bir NSG gerekir. Bu durumda, hello kullanmayı düşünmelisiniz **uygulama katmanı, uygulama başına Nsg'ler başına tek bir alt ağda** tasarım deseni. Aşağıdaki Hello şekilde gösterilmektedir hello temsil eden hello tasarım deseni hello kullanımını **ProdBU1US1** VNet.

![Her katman, uygulama katmanı başına başına bir NSG bir alt ağ](./media/virtual-network-vnet-plan-design-arm/figure11.png)

Ancak, aynı zamanda toocreate fazladan bir alt ağ hello sanal ağlar ve şirket içi veri merkezleri arasında hello VPN bağlantısı için gerekir. Ve her alt ağ için toospecify hello adres alanı gerekiyor. Aşağıdaki Hello şekilde gösteren örnek bir çözüm için **ProdBU1US1** VNet. Bu senaryo için her bir Vnet'teki çoğaltılır. Her renk farklı bir uygulama temsil eder.

![Örnek VNet](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**Erişim denetimi**

Merhaba aşağıdaki gereksinimleri olan ilgili tooaccess denetimi:

* Merhaba şirketin ağ grubun hello VNet yapılandırmasını üzerinde tam denetimi olmalıdır.
* Her iş birimi geliştiriciler yalnızca mümkün toodeploy VM'ler tooexisting alt olmalıdır.

Bu gereksinimlerine bağlı olarak, kullanıcıların team toohello yerleşik ağ hello ekleyebilirsiniz **ağ Katılımcısı** rol her Abonelikteki; ve her abonelik vermiş uygulama geliştiricileri hello için özel bir rol oluşturur bunları hak tooadd VM'ler tooexisting alt ağı.

## <a name="next-steps"></a>Sonraki adımlar
* [Bir sanal ağı dağıtmak](virtual-networks-create-vnet-arm-template-click.md) bir senaryoyu temel.
* Nasıl çok anlamak[Yük Dengelemesi](../load-balancer/load-balancer-overview.md) Iaas Vm'leri ve [üzerinde birden fazla Azure bölgesine yönlendirmesi yönetmek](../traffic-manager/traffic-manager-overview.md).
* Daha fazla bilgi edinmek [Nsg'ler ve nasıl tooplan ve tasarım](virtual-networks-nsg.md) bir NSG çözümü.
* Daha fazla bilgi edinmek, [şirket içi ve sanal ağ bağlantısı seçenekleri](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti).
