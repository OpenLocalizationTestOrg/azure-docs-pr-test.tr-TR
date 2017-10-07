---
title: "aaaUser tanımlı yollar ve IP iletimi azure'da | Microsoft Docs"
description: "Azure'da sanal gereçler toonetwork tooconfigure kullanıcı tanımlı yolları (UDR) ve IP iletimi tooforward nasıl trafiği öğrenin."
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
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>Kullanıcı tanımlı yollar ve IP iletme

Azure'da sanal makine (VM) tooa sanal ağ (VNet) eklediğinizde, hello VM'ler hello ağ üzerinden birbirleriyle mümkün toocommunicate otomatik olarak olduğunu fark edeceksiniz. Merhaba VM'ler olsa da farklı alt ağlarda bir ağ geçidi toospecify gerekmez. Merhaba aynı hello VM'ler toohello gelen iletişimi için doğru ortak Internet ve Azure tooyour karma bağlantısından sahip olduğunda datacenter varsa bile tooyour şirket içi ağ.

Azure bir dizi IP trafiğinin nasıl akacağını sistem yolları toodefine kullandığından bu iletişim akışını mümkündür. Sistem yolları senaryoları aşağıdaki hello iletişiminde hello akışını denetler:

* Aynı alt ağ içinden hello.
* Bir sanal ağ içindeki bir alt ağ tooanother.
* Sanal makineleri toohello ' Internet.
* Bir VNet tooanother sanal ağ VPN ağ geçidi üzerinden.
* Bir VNet tooanother VNet eşlemesi (hizmet zincirleme) aracılığıyla VNet.
* VNet tooyour şirket içi ağ üzerinden bir VPN ağ geçidi üzerinden.

Aşağıdaki Hello şekilde VNet, iki alt ağ ve birkaç VM'yi hello içeren basit bir kurulum IP trafiğinin tooflow izin sistem yolları gösterilmektedir.

![Azure'daki sistem yolları](./media/virtual-networks-udr-overview/Figure1.png)

Sistem yolları Hello kullanımını trafiği dağıtımınız için otomatik olarak kolaylaştırsa da, toocontrol hello bir sanal gereç yoluyla paketlerin yönlendirilmesini istediğiniz durumlar vardır. Bu nedenle, kullanıcı tanımlı yollar oluşturarak tooa belirli alt toogo tooyour sanal gereç yerine akan paketlerde için sonraki atlama hello belirtebilirsiniz ve IP iletme için hello hello sanal gereç olarak çalışan VM.

Kullanıcı tanımlı yollar örneğini aşağıdaki şekilde Hello gösterir ve tooforce paketleri iletme IP tooone alt üçüncü bir alt ağdaki sanal gereç aracılığıyla başka bir toogo gönderilir.

![Azure'daki sistem yolları](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> Kullanıcı tanımlı yolların (ağ arabirimleri tooVMs bağlı gibi) bir alt ağ hello alt ağda herhangi bir kaynağa bırakarak uygulanan tootraffic edilir. Yollar toospecify oluşturulamıyor nasıl trafiği bir alt ağ Internet hello örneği için girer. trafik toocannot iletme hello Gereci olması hello hello trafiğin kaynaklandığı aynı alt ağ. Gereçleriniz için her zaman ayrı bir alt ağ oluşturun. 
> 
> 

## <a name="route-resource"></a>Yol kaynağı
Paketler hello fiziksel ağdaki her düğümde tanımlanan bir yol tablosu temel bir TCP/IP ağı üzerinden yönlendirilir. Bir yol tablosu tek tek rota koleksiyonu toodecide nerede tooforward paketleri hello hedef sunucudaki IP adresi tabanlı kullanılır. Bir rota hello şunlardan oluşur:

| Özellik | Açıklama | Kısıtlamalar | Dikkat edilmesi gerekenler |
| --- | --- | --- | --- |
| Adres Ön Eki |Merhaba hedef CIDR toowhich hello rota 10.1.0.0/16 gibi uygulanır. |Merhaba üzerindeki adresleri temsil eden geçerli bir CIDR aralığı olmalıdır genel Internet, Azure sanal ağı veya şirket içi veri merkezi. |Merhaba emin olun **adres ön eki** hello için başlangıç adresi içermiyor **sonraki atlama adresi**, aksi takdirde paketlerinizi hello kaynak toohello sonraki atlama hiç varmadan bir döngüye girer Merhaba hedef. |
| Sonraki atlama türü |Azure atlama hello paket Hello türü gönderilmesi. |Değerleri aşağıdaki hello biri olmalıdır: <br/> **Sanal Ağ**. Merhaba yerel sanal ağı temsil eder. Örneğin, iki alt ağlarınız varsa, 10.1.0.0/16 ve 10.2.0.0/16 içinde Merhaba aynı sanal ağ, hello rota hello yol tablosundaki her alt ağ için bir sonraki atlama değeri olacaktır *sanal ağ*. <br/> **Sanal Ağ Geçidi**. Azure S2S VPN Gateway'i temsil eder. <br/> **İnternet**. Merhaba varsayılan Internet ağ geçidi Hello Azure altyapısı tarafından sağlanan temsil eder. <br/> **Sanal Gereç**. Azure sanal ağı tooyour eklediğiniz sanal Gereci temsil eder. <br/> **None**. Bir kara deliği temsil eder. Tooa kara delik iletilen paketler hiç iletilir değil. |Kullanmayı **sanal gereç** toodirect trafiği tooa VM veya Azure yük dengeleyici iç IP adresi.  Bu tür bir IP adresi aşağıda açıklandığı gibi hello belirtimi sağlar. Kullanmayı bir **hiçbiri** hedef verilen boyunca tooa toostop paketler yazın. |
| Sonraki atlama adresi |Merhaba sonraki atlama adresi paketlerin iletilmesi gereken hello IP adresini içerir. Sonraki atlama değerlerine yalnızca sonraki atlama türü hello olduğu yollarda izin *sanal gereç*. |Hello burada hello kullanıcı tanımlı yol uygulanır, oluşturulmak olmadan sanal ağ içinde erişilebilir bir IP adresi olmalıdır bir **sanal ağ geçidi**. Başlangıç IP adresi toobe aynı sanal ağ uygulandığı durumlarda hello veya eşlenmiş bir sanal ağ var. |Başlangıç IP adresi bir VM'yi temsil ediyorsa, etkinleştirdiğinizden emin olun [IP iletimini](#IP-forwarding) azure'da hello VM için. Merhaba IP adresini temsil hello iç IP adresi Azure yük dengeleyici, değişiklik yaparsanız eşleşen bir Yük Dengeleme kuralı her bağlantı noktası için sahip olduğunuzdan emin tooload Bakiye istiyor.|

Azure PowerShell'de bazı hello "NextHopType" değerlerinden farklı adlara sahip:

* Sanal Ağ VnetLocal şeklindedir
* Sanal Ağ Geçidi VirtualNetworkGateway şeklindedir
* Sanal Gereç VirtualAppliance şeklindedir
* İnternet, İnternet’tir
* None, None şeklindedir

### <a name="system-routes"></a>Sistem yolları
Bir sanal ağda oluşturulan her alt ağ hello aşağıdaki sistem yolu kurallarını içeren bir yol tablosu ile otomatik olarak ilişkilendirilir:

* **Yerel Sanal Ağ Kuralı**: Bu kural bir sanal ağdaki her alt ağ için otomatik olarak oluşturulur. Merhaba VNet içinde hello VM'ler arasında doğrudan bağlantı yoktur ve Ara sonraki atlama olduğunu belirtir.
* **Şirket içi kuralı**: Bu kural tooall hedefleyen trafiğe toohello şirket içi adres aralığı uygular ve VPN ağ geçidi hello sonraki atlama hedefi olarak kullanır.
* **Internet kuralı**: Bu kural tüm giden trafiğe toohello işleme ortak Internet (adres öneki 0.0.0.0/0) ve hello olarak kullandığı hello altyapı internet ağ geçidi sonraki tüm giden trafiğe toohello için Internet atlama.

### <a name="user-defined-routes"></a>Kullanıcı tanımlı yollar
Çoğu ortam için Azure'da zaten tanımlanmış hello sistem yolları yalnızca gerekir. Ancak, bir yol tablosu toocreate gerekir ve gibi belirli durumlarda, bir veya daha fazla yol eklemek:

* Şirket içi ağınız üzerinden tünel toohello Internet zorlar.
* Azure ortamınızda sanal gereçleri kullanma.

Merhaba yukarıdaki senaryolarda bir yol tablosu toocreate sahip ve kullanıcı tanımlı yollar tooit ekleyin. Birden fazla yol tablonuz olabilir ve hello aynı yol tablosu ilişkili tooone veya daha fazla alt ağlar olabilir. Ve her alt ağ yalnızca ilişkili tooa tek yol tablosu olabilir. Tüm VM'ler ve bulut Hizmetleri bir alt ağdaki hello rota ilişkili tablo toothat alt kullanın.

Bir yol tablosu ilişkili toohello alt kadar alt ağlar sistem yollarına bağımlıdır. Bir ilişki oluşturulduğu zaman, hem kullanıcı tanımlı yollar hem de sistem yolları arasında En Uzun Ön Ek Eşleşmesi (LPM) temel alınarak yönlendirme uygulanır. Varsa aynı LPM eşleşen bir rota seçili sonra hello sahip birden fazla yol sırasının Merhaba, özgün temel:

1. Kullanıcı tanımlı yol
2. BGP yolu (ExpressRoute kullanıldığında)
3. Sistem yolu

toolearn toocreate kullanıcı tanımlı yollar, nasıl bkz [nasıl tooCreate yönlendirir ve azure'da IP iletimini etkinleştirmeniz](virtual-network-create-udr-arm-template.md).

> [!IMPORTANT]
> Kullanıcı tanımlı yollar yalnızca uygulanan tooAzure VM'ler olan ve bulut Hizmetleri. Tooadd şirket içi ağınız ve Azure arasında bir güvenlik duvarı sanal Gereci isterseniz, örneğin, toocreate toohello şirket içi adres alanı toohello sanal giden tüm trafiği ileten bir kullanıcı tanımlı yol Azure yol tablolarınız için gerekir Gereci. Ayrıca, bir kullanıcı rota (UDR) toohello GatewaySubnet tooforward hello sanal gereç yoluyla şirket içi tooAzure gelen tüm trafiği tanımlanan ekleyebilirsiniz. Bu, kısa süre önce yapılan bir eklemedir.
> 
> 

### <a name="bgp-routes"></a>BGP yolları
Şirket içi ağınız ve Azure arasında bir ExpressRoute bağlantınız varsa, şirket içi ağ tooAzure BGP toopropagate yollarını etkinleştirebilirsiniz. Bu BGP yolları hello kullanılan aynı şekilde sistem yollarıyla ve kullanıcı tanımlı yollar her Azure alt. Daha fazla bilgi için bkz. [ExpressRoute'a Giriş](../expressroute/expressroute-introduction.md).

> [!IMPORTANT]
> Şirket içi ağınızdan hello sonraki atlama olarak hello VPN ağ geçidini kullanan 0.0.0.0/0 alt ağ için bir kullanıcı tanımlı yol oluşturarak tünel Azure ortamı toouse ekibinizin yapılandırabilirsiniz. Ancak bu işlem yalnızca ExpressRoute yerine bir VPN ağ geçidini kullandığınız zaman çalışır. ExpressRoute için zorlamalı tünel BGP yoluyla yapılandırılır.
> 
> 

## <a name="ip-forwarding"></a>IP iletimi
Merhaba nedenler toocreate birini yukarıda açıklandığı gibi bir kullanıcı tanımlı yol tooforward trafiği tooa sanal gereç özelliğidir. Bir sanal gereç kullanılan uygulama toohandle ağ trafiğinin bir güvenlik duvarı veya NAT cihazı gibi herhangi bir şekilde çalışan bir VM'den fazla bir şey değildir.

Bu sanal gereç VM olan mümkün tooreceive gelen trafiği olmalıdır tooitself ele değil. tooallow VM tooreceive trafik tooother hedefleri ele, IP iletimi hello VM için etkinleştirmeniz gerekir. Bu ayar, bir ayar değildir hello konuk işletim sistemindeki bir Azure olur.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[hello Resource Manager dağıtım modelinde yollar oluşturmayı](virtual-network-create-udr-arm-template.md) ve toosubnets ilişkilendirebilirsiniz. 
* Nasıl çok öğrenin[hello Klasik dağıtım modelinde yollar oluşturmayı](virtual-network-create-udr-classic-ps.md) ve toosubnets ilişkilendirebilirsiniz.

