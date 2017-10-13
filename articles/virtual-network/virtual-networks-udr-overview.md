---
title: "Azure'da kullanıcı tanımlı rotalar ve IP İletimi | Microsoft Docs"
description: "Azure'da trafiği ağ sanal gereçlerine iletmek için kullanıcı tanımlı yolları (UDR) ve IP İletimini nasıl yapılandıracağınızı öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6274e0101f6fb0864c8d1efaef7fcde78b8760c3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>Kullanıcı tanımlı yollar ve IP iletme

Azure'da bir sanal ağa (VNet) sanal makineler (VM'ler) eklediğiniz zaman, VM'lerin birbirleri ile ağ üzerinde otomatik olarak iletişim kurabildiklerini fark edersiniz. VM'ler farklı alt ağlarda bulunsa bile bir ağ geçidini belirtmenize gerek yoktur. Aynı şey VM'lerden genel İnternet'e giden iletişimlerde ve hatta Azure'dan kendi veri merkezinize karma bir bağlantı bulunduğunda şirket içi ağınıza giden iletişimlerde de geçerlidir.

Bu iletişim akışının mümkün olmasını sağlayan şey, Azure'ın IP trafiğinin nasıl akacağını belirlemek için kullandığı bir dizi sistem yoludur. Sistem yolları aşağıdaki senaryolarda iletişim akışını denetler:

* Aynı alt ağ içinden.
* Bir sanal ağ içinde bir alt ağdan başka bir alt ağa.
* VM'lerden İnternet'e.
* Bir VPN ağ geçidi yoluyla bir sanal ağdan başka bir sanal ağa.
* Sanal Ağ Eşleme (Hizmet Zinciri) yoluyla bir sanal ağdan başka bir sanal ağa.
* Bir VPN ağ geçidi yoluyla bir sanal ağdan şirket içi ağınıza.

Aşağıdaki şekilde bir sanal ağı, iki alt ağı, birkaç VM'yi ve IP trafiğinin akmasını sağlayan sistem yollarını içeren basit bir kurulum gösterilmektedir.

![Azure'daki sistem yolları](./media/virtual-networks-udr-overview/Figure1.png)

Sistem yollarının kullanımı dağıtımınız için trafiği otomatik olarak kolaylaştırsa da, bir sanal gereç yoluyla paketlerin yönlendirilmesini denetlemek isteyeceğiniz durumlar vardır. Bunun için paketlerin belirli bir alt ağa akmak yerine bir sonraki atlamada sanal gerecinize gitmelerini belirten ve sanal gereç olarak çalışan VM için IP iletimini etkinleştiren kullanıcı tanımlı yollar oluşturabilirsiniz.

Aşağıdaki şekilde, bir alt ağdan başka bir alt ağa gönderilen paketleri üçüncü bir alt ağdaki sanal gereçten geçmeye zorlayan kullanıcı tanımlı yolların ve IP iletiminin bir örneği gösterilmektedir.

![Azure'daki sistem yolları](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> Kullanıcı tanımlı yollar, alt ağdaki herhangi bir kaynaktan (VM’lere eklenen ağ arabirimleri gibi) alt ağdan çıkan trafiğe uygulanır. Örneğin, İnternet’ten alt ağa trafiğin nasıl girdiğini belirtmek için rotalar oluşturamazsınız. Trafiği ilettiğiniz gereç, trafiğin kaynaklandığı alt ağda yer alamaz. Gereçleriniz için her zaman ayrı bir alt ağ oluşturun. 
> 
> 

## <a name="route-resource"></a>Yol kaynağı
Paketler, fiziksel ağdaki her düğümde tanımlanan bir yol tablosu temel alınarak bir TCP/IP ağı üzerinden yönlendirilir. Yol tablosu, hedef IP adresine göre paketlerin nereye iletileceğine karar veren bir tekil yollar koleksiyonudur. Bir yol aşağıdakilerden oluşur:

| Özellik | Açıklama | Kısıtlamalar | Dikkat edilmesi gerekenler |
| --- | --- | --- | --- |
| Adres Ön Eki |Yolun uygulandığı hedef CIDR'si, ör. 10.1.0.0/16. |Genel İnternet, Azure sanal ağı veya şirket içi veri merkezi üzerindeki adresleri temsil eden geçerli bir CIDR aralığı olmalıdır. |**Adres ön ekinin** **Nexthop adresini** içermediğinden emin olun, aksi halde kaynaktan bir sonraki atlamaya giden paketleriniz hedefe hiç varmadan bir döngüye girer. |
| Sonraki atlama türü |Paketin gönderilmesi gereken Azure atlama türü. |Aşağıdaki değerlerden biri olmalıdır: <br/> **Sanal Ağ**. Yerel sanal ağı temsil eder. Örneğin, aynı sanal ağ içinde 10.1.0.0/16 ve 10.2.0.0/16 şeklinde iki alt ağınız varsa yol tablosundaki her alt ağ yolunun bir sonraki atlama değeri *Sanal Ağ* olur. <br/> **Sanal Ağ Geçidi**. Azure S2S VPN Gateway'i temsil eder. <br/> **İnternet**. Azure Altyapısı tarafından sağlanan varsayılan İnternet ağ geçidini temsil eder. <br/> **Sanal Gereç**. Azure sanal ağınıza eklediğiniz sanal gereci temsil eder. <br/> **None**. Bir kara deliği temsil eder. Bir kara deliğe iletilen paketler aktarılmaz. |Trafiği bir VM veya Azure Load Balancer iç IP adresine yönlendirmek için **Sanal Gereç** kullanabilirsiniz.  Bu tür, aşağıda belirtilen şekilde bir IP adresinin belirtilmesini sağlar. Paketlerin belirli bir hedefe akmasını durdurmak için bir **None** türünü kullanmayı değerlendirin. |
| Sonraki atlama adresi |Sonraki atlama adresi, paketlerin iletilmesi gereken IP adresini içerir. Yalnızca sonraki atlama türünün *Sanal Gereç* olduğu yollarda sonraki atlama değerlerine izin verilir. |Bir **Sanal Ağ Geçidi**’nden geçmeden Kullanıcı Tanımlı Yolun uygulandığı Sanal Ağ içerisinde erişilebilir bir IP adresi olmalıdır. IP adresi, uygulandığı Sanal Ağ üzerinde veya eşlenmiş bir Sanal Ağ üzerinde olmalıdır. |IP adresi bir VM'yi temsil ediyorsa Azure'da VM için [IP iletimini](#IP-forwarding) etkinleştirdiğinizden emin olun. IP adresi, Azure Load Balancer'ın iç IP adresini temsil ediyorsa, yük dengeleme yapmak istediğiniz her bağlantı noktasına karşılık gelen bir yük dengeleme kuralına sahip olduğunuzdan emin olun.|

Azure PowerShell’de "NextHopType" değerlerinin bazıları farklı adlara sahiptir:

* Sanal Ağ VnetLocal şeklindedir
* Sanal Ağ Geçidi VirtualNetworkGateway şeklindedir
* Sanal Gereç VirtualAppliance şeklindedir
* İnternet, İnternet’tir
* None, None şeklindedir

### <a name="system-routes"></a>Sistem yolları
Bir sanal ağda oluşturulan her alt ağ, aşağıdaki sistem yolu kurallarını içeren bir yol tablosu ile otomatik olarak ilişkilendirilir:

* **Yerel Sanal Ağ Kuralı**: Bu kural bir sanal ağdaki her alt ağ için otomatik olarak oluşturulur. Sanal ağ içindeki VM'ler arasında doğrudan bir bağlantı olduğunu ve ara sonraki atlama bulunmadığını belirtir.
* **Şirket İçi Kuralı**: Bu kural şirket içi adres aralığına giden tüm trafiğe uygulanır ve sonraki atlama hedefi olarak VPN ağ geçidini kullanır.
* **İnternet Kuralı**: Bu kural, genel İnternet'e (adres ön eki: 0.0.0.0/0) giden tüm trafiği işler ve İnternet'e giden tüm trafik için sonraki durak olarak İnternet ağ geçidi altyapısını kullanır.

### <a name="user-defined-routes"></a>Kullanıcı tanımlı yollar
Çoğu ortam için ihtiyaç duyacağınız tek şey, Azure'da zaten tanımlanmış olan sistem yollarıdır. Ancak belirli durumlarda bir yol tablosu oluşturmanız ve bir veya daha fazla yol eklemeniz gerekebilir, örneğin:

* Şirket içi ağınız yoluyla İnternet'e zorlamalı tünel uygulama.
* Azure ortamınızda sanal gereçleri kullanma.

Yukarıdaki senaryolarda bir yol tablosu oluşturmanız ve buna kullanıcı tanımlı yollar eklemeniz gerekir. Birden fazla yol tablonuz olabilir ve bir yol tablosu bir veya daha fazla alt ağ ile ilişkilendirilebilir. Bununla birlikte her alt ağ yalnızca tek bir yol tablosu ile ilişkilendirilebilir. Bir alt ağda bulunan tüm VM'ler ve bulut hizmetleri bu alt ağ ile ilişkilendirilen yol tablosunu kullanır.

Yol tablosu bir alt ağ ile ilişkilendirilene kadar alt ağlar sistem yollarına bağımlıdır. Bir ilişki oluşturulduğu zaman, hem kullanıcı tanımlı yollar hem de sistem yolları arasında En Uzun Ön Ek Eşleşmesi (LPM) temel alınarak yönlendirme uygulanır. Aynı LPM eşleşmesine sahip birden fazla yol bulunuyorsa yol aşağıdaki sırayla ve kaynağına göre seçilir:

1. Kullanıcı tanımlı yol
2. BGP yolu (ExpressRoute kullanıldığında)
3. Sistem yolu

Kullanıcı tanımlı yolların nasıl oluşturulacağını öğrenmek için bkz. [Azure'da Yollar Oluşturma ve IP İletimini Etkinleştirme](virtual-network-create-udr-arm-template.md).

> [!IMPORTANT]
> Kullanıcı tanımlı yollar yalnızca Azure VM'leri ve bulut hizmetleri için uygulanır. Örneğin, şirket içi ağınız ve Azure arasında bir güvenlik duvarı sanal gereci eklemek isterseniz Azure yol tablolarınız için şirket içi adres alanına giden tüm trafiği sanal gerece ileten bir yol oluşturmanız gerekir. Şirket içinden gelen tüm trafiği sanal gereç aracılığıyla Azure'a iletmek için GatewaySubnet'e kullanıcı tanımlı bir yol da (UDR) ekleyebilirsiniz. Bu, kısa süre önce yapılan bir eklemedir.
> 
> 

### <a name="bgp-routes"></a>BGP yolları
Şirket içi ağınız ve Azure arasında bir ExpressRoute bağlantınız varsa BGP'yi etkinleştirerek şirket içi ağınızdan Azure'a giden yollar yayabilirsiniz. Bu BGP yolları, her Azure alt ağında yer alan sistem yollarıyla ve kullanıcı tanımlı yollarla aynı şekilde kullanılır. Daha fazla bilgi için bkz. [ExpressRoute'a Giriş](../expressroute/expressroute-introduction.md).

> [!IMPORTANT]
> Şirket içi ağınızda zorlamalı tünel kullanmak üzere Azure ortamınızı yapılandırabilirsiniz, bunun için sonraki atlama olarak VPN ağ geçidini kullanan 0.0.0.0/0 alt ağı için kullanıcı tanımlı bir yol oluşturun. Ancak bu işlem yalnızca ExpressRoute yerine bir VPN ağ geçidini kullandığınız zaman çalışır. ExpressRoute için zorlamalı tünel BGP yoluyla yapılandırılır.
> 
> 

## <a name="ip-forwarding"></a>IP iletimi
Yukarıda açıklanan şekilde, kullanıcı tanımlı bir yol oluşturmanın temel nedenlerinden biri de trafiği bir sanal gerece iletmektir. Sanal gereç, güvenlik duvarı veya NAT cihazı gibi ağ trafiğini işlemek için kullanılan bir uygulamayı çalıştıran bir VM'den fazlası değildir.

Bu sanal gereç VM'si, kendisine yönelik olmayan gelen trafiği alabilmelidir. Bir VM'nin başka hedeflere yönelik trafiği alabilmesine izin vermek için VM'de IP İletimini etkinleştirmeniz gerekir. Bu ayar konuk işletim sisteminin değil, Azure'ın bir ayarıdır.

## <a name="next-steps"></a>Sonraki adımlar
* [Resource Manager dağıtım modelinde yollar oluşturmayı](virtual-network-create-udr-arm-template.md) ve bunları alt ağlar ile ilişkilendirmeyi öğrenin. 
* [Klasik dağıtım modelinde yollar oluşturmayı](virtual-network-create-udr-classic-ps.md) ve bunları alt ağlar ile ilişkilendirmeyi öğrenin.

