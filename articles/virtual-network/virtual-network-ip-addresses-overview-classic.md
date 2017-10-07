---
title: "aaaIP adres türleri Azure (Klasik) | Microsoft Docs"
description: "Azure ortak ve özel IP adresleri (Klasik) hakkında bilgi edinin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>IP adresi türleri ve ayırma yöntemleri (Azure'da Klasik)
IP adreslerini tooAzure kaynakları toocommunicate şirket içi ağınızı Azure diğer kaynaklarla atayın ve Internet hello. Azure'da kullanabileceğiniz IP adreslerinin iki tür vardır: ortak ve özel.

Genel IP adresleri hello Azure genel kullanıma yönelik Hizmetleri dahil olmak üzere Internet ile iletişim için kullanılır.

Ağ tooAzure bir VPN ağ geçidi veya ExpressRoute bağlantı hattı tooextend kullandığınızda özel IP adresleri bir Azure sanal ağı (VNet), bir bulut hizmeti ve şirket içi ağınız içinde iletişim için kullanılır.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).  Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların Resource Manager kullanmanızı önerir. IP adresleriyle Kaynak Yöneticisi'nde hello okuma hakkında bilgi edinin [IP adreslerini](virtual-network-ip-addresses-overview-arm.md) makalesi.

## <a name="public-ip-addresses"></a>Genel IP adresleri
Genel IP adreslerine izin Internet ve Azure genel kullanıma yönelik Hizmetleri ile Azure kaynaklarını toocommunicate gibi [Azure Redis önbelleği](https://azure.microsoft.com/services/cache/), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [SQL veritabanları](../sql-database/sql-database-technical-overview.md), ve [Azure depolama](../storage/common/storage-introduction.md).

Bir ortak IP adresi şu kaynak türlerini hello ile ilişkilidir:

* Bulut hizmetleri
* Iaas sanal makineleri (VM'ler)
* PaaS rolü örnekleri
* VPN ağ geçitleri
* Uygulama ağ geçitleri

### <a name="allocation-method"></a>Ayırma yöntemi
Bir ortak IP adresi tooan Azure kaynak atanan toobe gerektiğinde olan *dinamik olarak* ayrılan kullanılabilir genel IP havuzundan hello konumu hello kaynak içinde bir adres oluşturdu. Merhaba kaynak durdurulduğunda bu IP adresi serbest bırakılır. Tüm hello rolü örnekleri durduğunda böyle bir bulut hizmeti olan durumunda, hangi kaçınılabilir kullanarak bir *statik* (ayrılmış) IP adresi (bkz [bulut Hizmetleri](#Cloud-services)).

> [!NOTE]
> IP aralıklarını, genel IP adresleri tooAzure kaynakları ayrılır Hello listesi konumunda yayımlanır [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

### <a name="dns-hostname-resolution"></a>DNS ana bilgisayar adı çözümlemesi
Bir bulut hizmeti veya bir Iaas VM oluşturduğunuzda, tooprovide tüm Azure kaynakları arasında benzersiz olan bir bulut hizmeti DNS adı gerekiyor. Bu eşleme hello Azure tarafından yönetilen DNS sunucuları için oluşturur *dnsname*. hello kaynak cloudapp.net toohello genel IP adresi. Örneğin, oluşturduğunuzda, bir bulut hizmeti bir bulut hizmeti DNS adı ile **contoso**, hello tam etki alanı adı (FQDN) **contoso.cloudapp.net** tooa genel IP adresi (VIP) çözümler Merhaba bulut hizmeti. Bu FQDN toocreate Azure'da toohello genel IP adresine işaret eden bir özel etki alanı CNAME kaydı kullanabilirsiniz.

### <a name="cloud-services"></a>Bulut hizmetleri
Bir bulut hizmeti her zaman bir ortak IP başvurulan tooas bir sanal IP adresi (VIP) adresi vardır. Uç noktaları bir bulut hizmeti tooassociate farklı bağlantı noktaları hello VIP toointernal noktalarına VM'ler ve rol örnekleri hello bulut hizmeti içinde oluşturabilirsiniz. 

PaaS rolü örnekleri, aracılığıyla sunulan tüm aynı bulut hizmeti VIP hello ya bir bulut hizmeti birden çok Iaas Vm'leri içerebilir. Ayrıca atayabilirsiniz [birden çok VIP'ler tooa bulut hizmeti](../load-balancer/load-balancer-multivip.md), çok kiracılı ortamı SSL tabanlı Web sitelerinde gibi çoklu VIP senaryoları etkinleştirir.

Hello genel IP adresi, bir bulut Hizmeti'nin aynı, hatta tüm rol örneklerinin hello olduğunda durdurulur, kullanarak hello kaldığından emin olmak bir *statik* ortak IP adresi, başvurulan tooas [ayrılmış IP](virtual-networks-reserved-public-ip.md). Belirli bir konumda statik (ayrılmış) IP kaynağı oluşturun ve o konumda tooany bulut hizmeti atayın. Merhaba ayrılmış IP'si için hello gerçek IP adresi belirtemezsiniz, oluşturulduktan hello konumda kullanılabilir IP adresi havuzundan ayrılan. Açıkça silene kadar bu IP adresi serbest bırakılmaz.

Statik (ayrılmış) ortak IP adresleri, genellikle bir bulut hizmeti burada hello senaryolarda kullanılır:

* güvenlik duvarı kuralları toobe Kurulum, son kullanıcılar tarafından gerektirir.
* dış DNS ad çözümlemesi bağlıdır ve dinamik IP A kayıtlarını güncelleştirme gerektirir.
* IP tabanlı güvenlik modeli kullanan dış web hizmetlerini kullanır.
* SSL sertifikaları bağlantılı tooan IP adresini kullanır.

> [!NOTE]
> Bir kapsayıcı klasik bir VM oluştururken *bulut hizmeti* bir sanal IP adresi (VIP) olan Azure tarafından oluşturulur. Merhaba oluşturma RDP veya SSH varsayılan portal yapılır zaman *endpoint* hello bulut hizmeti VIP toohello VM bağlanabilmesi için hello portal tarafından yapılandırılır. Ayrılmış IP adresi tooconnect toohello VM etkili bir şekilde sağlayan bu bulut hizmeti VIP ayrılabilir. Daha fazla uç noktaları yapılandırarak ek bağlantı noktalarını açabilirsiniz.
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>Iaas Vm'leri ve PaaS rol örnekleri
Bir ortak atayabilirsiniz IP adresi doğrudan tooan Iaas [VM](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya PaaS rolü örneğini bir bulut hizmeti içinde. Başvurulan tooas bir örnek düzeyinde ortak IP adresi budur ([ILPIP](virtual-networks-instance-level-public-ip.md)). Bu genel IP adresi yalnızca dinamik olabilir.

> [!NOTE]
> Bu hello VIP Iaas Vm'si veya PaaS rol örnekleri için bir kapsayıcıdır hello bulut hizmetinin farklıdır, bir bulut hizmeti birden çok Iaas Vm'si veya PaaS rolü örnekleri, hello sunulan tüm içerebileceğinden aynı hizmet VIP bulut.
> 
> 

### <a name="vpn-gateways"></a>VPN ağ geçitleri
A [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md) kullanılan tooconnect Azure VNet tooother Azure Vnet veya şirket içi ağlar olabilir. Bir VPN ağ geçidi genel bir IP adresi atanır *dinamik olarak*, hello uzak ağ ile iletişim sağlar.

### <a name="application-gateways"></a>Uygulama ağ geçitleri
Bir Azure [uygulama ağ geçidi](../application-gateway/application-gateway-introduction.md) tooroute ağ trafiğinin Yük Dengeleme HTTP tabanlı Layer7 için kullanılabilir. Uygulama ağ geçidi, bir ortak IP adresi atanır *dinamik olarak*, yük dengeli VIP hello olarak sunar.

### <a name="at-a-glance"></a>Bir bakışta
Merhaba tabloda birden çok ortak IP adresleri hello ayırma yöntemlerini (dinamik/statik) ve yeteneği tooassign ile her kaynak türünü gösterir.

| Kaynak | Dinamik | Statik | Birden çok IP adresi |
| --- | --- | --- | --- |
| Bulut hizmeti |Evet |Evet |Evet |
| Iaas VM veya PaaS rol örneği |Evet |Hayır |Hayır |
| VPN ağ geçidi |Evet |Hayır |Hayır |
| Uygulama ağ geçidi |Evet |Hayır |Hayır |

## <a name="private-ip-addresses"></a>Özel IP adresleri
Özel IP adresleri izin Azure kaynaklarını toocommunicate diğer kaynaklara sahip bir bulut hizmetinde veya bir [sanal ağ](virtual-networks-overview.md)(VNet) veya kullanmadan tooon içi ağından (bir VPN ağ geçidi veya expressroute bağlantı hattı), bir Internet erişilebilir bir IP adresi.

Azure Klasik dağıtım modelinde, özel bir IP adresi Azure kaynaklarını aşağıdaki toohello atanabilir:

* Iaas Vm'leri ve PaaS rol örnekleri
* İç yük dengeleyici
* Uygulama ağ geçidi

### <a name="iaas-vms-and-paas-role-instances"></a>Iaas Vm'leri ve PaaS rol örnekleri
Merhaba Klasik dağıtım modeliyle oluşturulan sanal makineleri (VM'ler) her zaman bir bulut hizmetinde benzer tooPaaS rol örnekleri yerleştirilir. Merhaba davranışı özel IP adresleri, böylece bu kaynaklar için benzer.

Bir bulut hizmeti olabilir önemli toonote olan iki yolla dağıtılabilir:

* Farklı bir *tek başına* bulut olduğu olmayan bir sanal ağ içindeki hizmeti.
* Sanal ağın bir parçası olarak.

#### <a name="allocation-method"></a>Ayırma yöntemi
Durumunda, bir *tek başına* bulut hizmeti, özel bir IP adresi ayrılan kaynakları get *dinamik olarak* hello Azure veri merkezinde özel bir IP adresi aralığı. Kullanılabilmesi için aynı bulut hizmeti yalnızca hello içindeki diğer VM'ler ile iletişim için. Merhaba kaynak durduruldu ve başlatılmışsa bu IP adresi değiştirebilirsiniz.

Bir sanal ağ içinde dağıtılan bir bulut hizmeti olan kaynakları özel alma durumunda hello adres aralığından hello ayrılan IP adresleri (belirtildiği gibi ağ yapılandırmasıyla) alt ağı ilişkilendirilmiş. Bu özel IP adresleri hello VNet içindeki tüm sanal makineler arasındaki iletişim için kullanılabilir.

Ayrıca, bir sanal ağ içindeki bulut Hizmetleri durumunda özel bir IP adresi ayrılır *dinamik olarak* (DHCP kullanarak) varsayılan olarak. Merhaba kaynak durduruldu ve başlatılmışsa değiştirebilirsiniz. tooensure başlangıç IP adresi kalır aynı Merhaba, tooset hello ayırma yöntemi çok gereksinim*statik*ve hello karşılık gelen adres aralığı içinde geçerli bir IP adresi sağlayın.

Statik özel IP adresleri yaygın olarak şunlar için kullanılır:

* Etki alanı denetleyicisi veya DNS sunucusu olarak çalışan VM’ler.
* IP adresleri kullanarak güvenlik duvarı kuralları gerektiren VM'ler.
* IP adresi üzerinden diğer uygulamalar tarafından erişilen Hizmetleri çalıştıran VM'ler.

#### <a name="internal-dns-hostname-resolution"></a>İç DNS ana bilgisayar adı çözümlemesi
Tüm Azure Vm'leri ve PaaS rol örnekleri ile yapılandırılan [Azure tarafından yönetilen DNS sunucuları](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) varsayılan olarak, özel DNS sunucularını açıkça yapılandırmadığınız sürece. Bu DNS sunucularına VM'ler için dahili ad çözümlemesi sağlamak ve aynı sanal veya Bulut hizmeti bulunan rol örnekleri hello.

Bir VM oluştururken hello hostname tooits özel IP adresi için bir eşleme toohello Azure tarafından yönetilen DNS sunucuları eklenir. Multi-NIC VM durumunda hello hostname eşlendi hello birincil NIC toohello özel IP adresi Ancak, bu eşleme bilgilerini kısıtlı tooresources olan hizmet veya sanal ağ içinde hello aynı bulut.

Durumunda, bir *tek başına* bulut hizmeti, mümkün tooresolve ana bilgisayar adları olacaktır aynı bulut hizmeti yalnızca hello içindeki tüm VM'ler/rol örnekleri. Bir sanal ağ içindeki bir bulut hizmeti durumunda hello VNet içindeki tüm hello VM'ler/rol örneklerinin mümkün tooresolve ana bilgisayar adı olacaktır.

### <a name="internal-load-balancers-ilb--application-gateways"></a>İç yük dengeleyiciler (ILB) ve Uygulama ağ geçitleri
Özel bir IP adresi toohello atayabilirsiniz **ön uç** yapılandırmasını bir [Azure iç yük dengeleyici](../load-balancer/load-balancer-internal-overview.md) (ILB) veya bir [Azure uygulama ağ geçidi](../application-gateway/application-gateway-introduction.md). Bu özel bir IP adresi iç uç noktası olarak hizmet veren, sanal ağ (VNet) ve hello uzak ağlar içinde erişilebilir yalnızca toohello kaynakları toohello VNet bağlanır. Ya da bir dinamik veya statik özel IP adresi toohello ön uç yapılandırması atayabilirsiniz. Ayrıca, birden çok özel IP adresleri tooenable çoklu vip senaryolar de atayabilirsiniz.

### <a name="at-a-glance"></a>Bir bakışta
Merhaba tabloda birden fazla özel IP adresleri hello ayırma yöntemlerini (dinamik/statik) ve yeteneği tooassign ile her kaynak türünü gösterir.

| Kaynak | Dinamik | Statik | Birden çok IP adresi |
| --- | --- | --- | --- |
| VM (içinde bir *tek başına* bulut hizmeti) |Evet |Evet |Evet |
| PaaS rolü örneğini (içinde bir *tek başına* bulut hizmeti) |Evet |Hayır |Evet |
| VM veya PaaS rol örneğinde (VNet) |Evet |Evet |Evet |
| İç yük dengeleyici ön uç |Evet |Evet |Evet |
| Uygulama ağ geçidi ön uç |Evet |Evet |Evet |

## <a name="limits"></a>Sınırlar
Merhaba tabloda Azure abonelik başına adresleme hello sınır IP uygulanmaz gösterir. Yapabilecekleriniz [desteğine başvurun](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooincrease hello varsayılan sınırları iş gereksinimlerinize göre toohello maksimum sınırlarını ayarlama.

|  | Varsayılan limit | Üst sınır |
| --- | --- | --- |
| Genel IP adresleri (dinamik) |5 |desteğe başvurun |
| Ayrılmış genel IP adresleri |20 |desteğe başvurun |
| Genel VIP her dağıtımda (bulut hizmeti) |5 |desteğe başvurun |
| Özel VIP (ILB) her dağıtımda (bulut hizmeti) |1 |1 |

Merhaba kümesini okuma olduğundan emin olun [sınırlar için ağ](../azure-subscription-service-limits.md#networking-limits) azure'da.

## <a name="pricing"></a>Fiyatlandırma
Çoğu durumda, genel IP adresleri ücretsizdir. Toouse ek ve/veya statik genel IP adresleri nominal bir ücret yoktur. Merhaba anladığınızdan emin olun [genel IP'ler için fiyatlandırma yapısına](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="differences-between-resource-manager-and-classic-deployments"></a>Resource Manager ve klasik dağıtımlar arasındaki farklar
Aşağıda Kaynak Yöneticisi ve hello Klasik dağıtım modeli IP adresleme özellikleri karşılaştırması verilmiştir.

|  | Kaynak | Klasik | Resource Manager |
| --- | --- | --- | --- |
| **Genel IP adresi** |***VM*** |Başvurulan tooas ILPIP (yalnızca dinamik) |Genel bir IP (dinamik veya statik) tooas adlandırılır |
|  ||Atanan tooan Iaas VM veya PaaS rol örneği |İlişkili toohello VM'in NIC | |
|  |***Internet'e yönelik Yük Dengeleyici*** |Başvurulan tooas VIP (dinamik) veya ayrılmış IP (statik) |Genel bir IP (dinamik veya statik) tooas adlandırılır | |
|  ||Atanan tooa bulut hizmeti |İlişkili toohello yük dengeleyicinin ön uç yapılandırma | |
|  | | | |
| **Özel IP adresi** |***VM*** |Başvurulan tooas DIP a |Başvurulan tooas özel bir IP adresi |
|  ||Atanan tooan Iaas VM veya PaaS rol örneği |Atanan toohello VM'in NIC | |
|  |***İç yük dengeleyiciye (ILB)*** |Atanan toohello ILB (dinamik veya statik) |Atanan toohello ILB'nin ön uç yapılandırma (dinamik veya statik) | |

## <a name="next-steps"></a>Sonraki adımlar
* [Özel bir statik IP adresi bir VM'yi dağıtmak](virtual-networks-static-private-ip-classic-pportal.md) hello Azure portal kullanarak.

