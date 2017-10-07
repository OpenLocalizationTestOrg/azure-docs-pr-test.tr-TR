---
title: "aaaAzure sanal ağ eşlemesi | Microsoft Docs"
description: "Azure'daki sanal ağ eşlemesi hakkında bilgi edinin."
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>Sanal ağ eşleme
Sanal ağ eşleme etkinleştirir, tooconnect iki sanal ağlarda aynı bölgede aracılığıyla hello Azure omurga ağı hello. Eşlendikten sonra hello iki sanal ağ bağlantısı amacıyla bir olarak görünür. Merhaba iki sanal ağlar hala ayrı kaynakları olarak yönetilebilir, ancak hello eşlenen sanal ağlar can sanal makinelerin birbirleriyle doğrudan, özel IP adresleri kullanarak iletişim.

Merhaba trafik hello içindeki sanal makineler arasında eşlenen sanal ağlar hello hello içindeki sanal makineler arasında trafik çok yönlendirilir gibi Azure altyapısı aracılığıyla yönlendirilir aynı sanal ağ. Sanal Ağ eşlemesi kullanmanın yararları hello bazıları şunlardır:

* Farklı sanal ağlardaki kaynaklar arasında düşük gecikme süresi ve yüksek bant genişlikli bağlantı.
* Ağ uygulamaları ve eşlenen bir sanal ağ içinde geçiş noktaları olarak VPN ağ geçitleri gibi Hello özelliği toouse kaynakları.
* Hello Azure Resource Manager dağıtım modeli aracılığıyla oluşturulan hello özelliği toopeer iki sanal ağ veya toopeer bir sanal ağ hello Klasik dağıtım modeli aracılığıyla oluşturulan Resource Manager tooa sanal ağ üzerinden oluşturuldu. Okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makale toolearn hello farklarını hello iki Azure dağıtım modelleri hakkında daha fazla bilgi.

## <a name="requirements-constraints"></a>Gereksinimler ve kısıtlamalar

* Merhaba eşlenen sanal ağlar hello aynı bulunmalıdır Azure bölgesi. Farklı Azure bölgelerindeki sanal ağları bir [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) kullanarak birbirine bağlayabilirsiniz.
* Merhaba eşlenen sanal ağlar çakışmayan bir IP adresi alanlarıyla olmalıdır.
* Bir sanal ağ başka bir sanal ağla eşlendikten sonra sanal ağa adres alanı eklenemez veya ağdaki bir adres alanı silinemez.
* Sanal ağ eşlemesi iki sanal ağ arasında gerçekleşir. Eşlemeler arasında türetilmiş geçişli bir ilişki yoktur. Örneğin, virtualNetworkA virtualNetworkB ile eşlenen ve virtualNetworkB virtualNetworkC ile eşlenen virtualNetworkA varsa, *değil* eşlenmiş toovirtualNetworkC.
* Uzun ayrıcalıklı bir kullanıcı olarak iki farklı Aboneliklerde bulunan sanal ağlar eş (bkz [özel izinler](create-peering-different-deployment-models-subscriptions.md#permissions)) hem abonelikleri yetkilendirir hello eşliği ve hello abonelikleri olan ilişkili toohello aynı Azure Active Directory kiracısı. Kullanabileceğiniz bir [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect sanal ağlar Aboneliklerde toodifferent Active Directory kiracıları ilişkilendirilmiş.
* Sanal ağlar, her ikisi de hello Resource Manager dağıtım modeli oluşturduysanız veya bir sanal ağı hello Resource Manager dağıtım modeli oluşturulur ve hello diğer hello Klasik dağıtım modeli aracılığıyla oluşturulursa eşlenemez. Merhaba Klasik dağıtım modeli aracılığıyla oluşturulan iki sanal ağ diğer, eşlenmiş tooeach ancak olamaz. Kullanabileceğiniz bir [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect iki sanal ağlar hello Klasik dağıtım modeli oluşturuldu.
* Merhaba iletişimi eşlenen sanal ağlardaki sanal makineler arasında hiçbir ek bant genişliği kısıtlaması içermese de en fazla ağ bant genişliği hala geçerli hello sanal makine boyutuna bağlı olarak yoktur. başka bir sanal makine boyutları, hello okumak için maksimum ağ bant genişliği hakkında daha fazla toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal makine boyutları makaleleri.
* Sanal makinelere yönelik Azure tarafından sağlanan iç DNS adı çözümlemesi, eşlenen sanal ağlarda kullanılamaz. Sanal makineler yalnızca hello yerel sanal ağ içinde çözümlenebilen iç DNS adlarına sahip. Ancak, sanal makineleri bağlı toopeered sanal ağlar bir sanal ağ için DNS sunucusu olarak yapılandırın. Daha fazla ayrıntı için hello okuma [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) makalesi.

![Temel sanal ağ eşleme](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>Bağlantı
İki sanal ağ eşlendikten sonra iki sanal ağınızdaki kaynaklara hello eşlenen sanal ağınızdaki kaynaklara ile doğrudan bağlanabilirsiniz. Merhaba iki sanal ağlara sahip olacak tam IP düzeyi bağlantısı.

Merhaba ağ gecikmesi için iki sanal makine eşlenen sanal ağlar arasındaki gidiş dönüş hello aynı tek bir sanal ağ içinde gidiş dönüş ettirilmesi. Merhaba ağ verimliliği ile orantılı tooits boyutu olan hello sanal makine için izin verilen hello bant genişliği temel alır. Merhaba eşliği içinde bant genişliği üzerinde başka bir kısıtlama yoktur.

Merhaba trafik eşlenen sanal ağlardaki sanal makineler arasında doğrudan hello bir ağ geçidi üzerinden değil Azure arka uç altyapısı aracılığıyla yönlendirilir.

Sanal makineler bağlı tooa sanal ağ hello iç yük dengeli uç nokta hello eşlenen sanal ağ erişebilir. Ağ güvenlik grupları sanal ağ tooblock erişim tooother sanal ağları veya alt ağlar, isterseniz uygulanabilir.

Sanal Ağ eşlemesi yapılandırırken, açın veya hello ağ güvenlik grubu kural hello sanal ağlar arasında kapatın. (Merhaba varsayılan seçenek olan) eşlenen sanal ağlar arasında tam bağlantı açarsanız, alt ağlar ya da sanal makineleri ağ güvenlik grupları toospecific tooblock uygulayabilir ya da belirli erişimini engellemek. Ağ güvenlik grupları hakkında daha fazla bilgi toolearn okuma hello [ağ güvenlik gruplarını genel bakış](virtual-networks-nsg.md) makalesi.

## <a name="service-chaining"></a>Hizmet zinciri
Kullanıcı tanımlı yollar bu noktası toovirtual makineler eşlenen sanal ağlarda "sonraki atlama" IP adresi: tooenable hizmet zincirleme hello şekilde yapılandırabilirsiniz. Hizmet zincirleme, kullanıcı tanımlı yollar ile eşlenmiş bir sanal ağ içindeki bir sanal ağ tooa sanal gerecin toodirect trafiği sağlar.

Ayrıca etkili bir şekilde hello hub altyapı bileşenlerini bir ağ sanal Gereci gibi barındırabildiği hub ve bağlı bileşen türü ortamları oluşturabilirsiniz. Tüm hello spoke sanal ağları sonra hello hub sanal ağla eş. Trafik hello hub sanal ağda çalışan sanal gereçler ağ üzerinden akabilir. Kısacası, sanal ağ eşlemesi hello sonraki atlama IP adresi hello kullanıcı tarafından tanımlanan rota toobe hello IP adresi hello eşlenen sanal ağındaki bir sanal makinenin üzerinde sağlar. Merhaba okuyun, kullanıcı tanımlı yollar hakkında daha fazla toolearn [kullanıcı tanımlı yollar genel bakış](virtual-networks-udr-overview.md) makalesi.

## <a name="gateways-and-on-premises-connectivity"></a>Ağ geçitleri ve şirket içi bağlantı
Yine de olup olmadığı başka bir sanal ağ ile eşlenen bağımsız olarak her sanal ağ kendi ağ geçidine sahip ve tooconnect tooan şirket içi ağ kullanın. Ayrıca yapılandırabilirsiniz [sanal ağ sanal ağ bağlantıları](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sanal ağlar eşlenmiş olsa bile, ağ geçitleri kullanarak.

Sanal ağ bağlantı için her iki seçenek yapılandırıldığında, hello sanal ağlar arasında trafiği hello hello eşleme yapılandırmasını akar (diğer bir deyişle, ile hello Azure omurga).

Sanal ağlar eşlendikleri olduğunda, bir geçiş noktası tooan şirket içi ağ olarak hello eşlenen sanal ağında hello ağ geçidi da yapılandırabilirsiniz. Bu durumda, uzak bir ağ geçidi kullanarak hello sanal ağ kendi ağ geçidine sahip olamaz. Bir sanal ağın yalnızca bir ağ geçidi olabilir. Merhaba ağ geçidi hello resim aşağıdaki gösterildiği gibi (Merhaba eşlenen sanal ağ içinde), yerel veya uzak gateway olabilir:

![VNet eşleme geçişi](./media/virtual-networks-peering-overview/figure02.png)

Ağ geçidi transit farklı dağıtım modeli oluşturulan sanal ağlar arasında hello eşleme ilişkisindeki desteklenmiyor. Merhaba eşleme ilişkisindeki her iki sanal ağlar Resource Manager aracılığıyla bir ağ geçidi transit toowork için oluşturulmuş olması gerekir.

Tek bir Azure ExpressRoute Bağlantısı Paylaşımı hello sanal ağlar eşlendikleri olduğunda, aralarında hello trafiği hello eşleme ilişkisindeki gider (diğer bir deyişle, ile hello Azure omurga ağı). Her sanal ağ tooconnect toohello şirket içi devredeki yerel ağ geçitlerini kullanmaya devam edebilirsiniz. Alternatif olarak, paylaşılan bir ağ geçidini kullanıp şirket içi bağlantı için bir geçiş yapılandırabilirsiniz.

## <a name="provisioning"></a>Sağlama
Sanal ağ eşlemesi ayrıcalıklı bir işlemdir. Merhaba VirtualNetworks ad alanı altındaki ayrı bir işlevdir. Bir kullanıcı belirli haklar tooauthorize eşliği verilebilir. Okuma-yazma erişimi toohello sanal ağ olan bir kullanıcı bu hakları otomatik olarak devralır.

Yönetici ya da bir kullanıcı ya da ayrıcalıklı kullanıcısı hello eşleme özelliğinin başka bir sanal ağ eşleme işlemi başlatabilir. Üzerinde eşleme için eşleşen bir istek varsa, diğer taraftaki hello ve diğer gereksinimler karşılanırsa hello eşleme kurulur.

## <a name="limits"></a>Sınırlar
Tek bir sanal ağı için izin verilen eşlemeler hello sayısı sınırlamaları vardır. Daha fazla bilgi için hello gözden [Azure ağ sınırlarına](../azure-subscription-service-limits.md#networking-limits).

## <a name="pricing"></a>Fiyatlandırma
Sanal ağ eşlemesi kullanan girdi ve çıktı trafiği için nominal bir ücret uygulanır. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-network).

## <a name="next-steps"></a>Sonraki adımlar

* Sanal ağ eşleme öğreticisini tamamlayın. Bir sanal ağ eşlemesi aynı hello oluşturulan sanal ağlar arasında oluşturulur veya aynı ya da farklı Aboneliklerde bulunan farklı dağıtım modellerini hello. Bir öğretici için senaryolar hello birini tamamlayın:
 
    |Azure dağıtım modeli  | Abonelik  |
    |---------|---------|
    |Her ikisi de Resource Manager |[Aynı](virtual-network-create-peering.md)|
    | |[Farklı](create-peering-different-subscriptions.md)|
    |Biri Resource Manager, diğeri klasik     |[Aynı](create-peering-different-deployment-models.md)|
    | |[Farklı](create-peering-different-deployment-models-subscriptions.md)|

* Bilgi nasıl toocreate bir [hub ve bağlı bileşen ağ topolojisi](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* Tüm hakkında bilgi edinin [sanal ağ eşleme ayarları ve nasıl toochange bunları](virtual-network-manage-peering.md)
