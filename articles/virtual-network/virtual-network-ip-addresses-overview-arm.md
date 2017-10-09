---
title: "azure'da aaaIP adres türleri | Microsoft Docs"
description: "Azure’da genel ve özel IP adresleri hakkında bilgi edinin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Azure’da IP adresi türleri ve ayırma yöntemleri
IP adreslerini tooAzure kaynakları toocommunicate şirket içi ağınızı Azure diğer kaynaklarla atayın ve Internet hello. Azure'da kullanabileceğiniz iki tür IP adresi vardır:

* **Genel IP adresleri**: hello Azure genel kullanıma yönelik Hizmetleri dahil olmak üzere Internet ile iletişim için kullanılan
* **Özel IP adresleri**: Azure sanal ağı (VNet) içinde iletişim için kullanılan ve şirket içi ağ tooAzure bir VPN ağ geçidi veya ExpressRoute bağlantı hattı tooextend kullandığınızda ağ.

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).  Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](virtual-network-ip-addresses-overview-classic.md).
> 

Merhaba Klasik dağıtım modeliyle bilginiz varsa, hello denetleyin [IP adresleme Klasik farklar ve Resource Manager](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Genel IP adresleri
Genel IP adreslerine izin Internet ve Azure genel kullanıma yönelik Hizmetleri ile Azure kaynaklarını toocommunicate gibi [Azure Redis önbelleği](https://azure.microsoft.com/services/cache/), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [SQL veritabanları](../sql-database/sql-database-technical-overview.md), ve [Azure depolama](../storage/common/storage-introduction.md).

Azure Resource Manager’daki bir [genel IP](resource-groups-networking.md#public-ip-address) adresi, kendi özelliklerine sahip olan bir kaynaktır. Genel bir IP adresi kaynağı herhangi bir kaynakları aşağıdaki hello ile ilişkilendirebilirsiniz:

* Sanal makineler (VM)
* İnternet'e yönelik yük dengeleyiciler
* VPN ağ geçitleri
* Uygulama ağ geçitleri

### <a name="allocation-method"></a>Ayırma yöntemi
Bir IP adresi tooa ayrılır iki yöntem vardır *ortak* IP kaynağı - *dinamik* veya *statik*. Merhaba varsayılan ayırma yöntemi *dinamik*, bir IP adresi olduğu **değil** Merhaba, oluşturma sırasında ayrılmış. Başlangıç (veya oluşturma) (örneğin, bir VM veya yük dengeleyici) ilişkili hello kaynak bunun yerine, hello genel IP adresi ayrılır. Durdur (veya silme olduğunda) hello kaynak hello IP adresi serbest bırakılır. Durdurma ve kaynak başlatma olduğunda bu başlangıç IP adresi toochange neden olur.

tooensure başlangıç IP adresi hello ilişkili kaynak kalır Merhaba aynı, hello ayırma yöntemi açıkça çok ayarlayabileceğiniz*statik*. Bu durumda, bir IP adresi anında atanır. Yalnızca hello kaynağı silme veya onun ayırma yöntemini çok değiştirdiğinizde yayımlanan*dinamik*.

> [!NOTE]
> Hatta hello ayırma yöntemi çok ayarladığınızda*statik*, hello gerçek IP adresi atanmış toohello belirtemezsiniz *genel IP kaynağı*. Bunun yerine, ayrılan hello Azure konumu IP adresi havuzundan hello kaynak oluşturulur.
>

Statik genel IP adresleri senaryoları aşağıdaki hello yaygın olarak kullanılır:

* Son kullanıcılar tooupdate güvenlik duvarı kuralları toocommunicate Azure kaynaklarınızı ile gerekir.
* IP adresindeki bir değişikliğin A kayıtlarının güncelleştirilmesini gerektireceği DNS ad çözümlemesi.
* Azure kaynaklarınız, IP adresi tabanlı bir güvenlik yöntemi kullanan diğer uygulama ve hizmetlerle iletişim kurar.
* SSL sertifikaları bağlantılı tooan IP adresi kullanın.

> [!NOTE]
> IP aralıklarını, genel IP adresleri (dinamik/statik) tooAzure kaynakları ayrılır Hello listesi konumunda yayımlanır [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>DNS ana bilgisayar adı çözümlemesi
Bir DNS etki alanı adı etiketi için bir eşleme oluşturur genel bir IP kaynağı için belirttiğiniz *domainnamelabel*. *Konum*. hello Azure tarafından yönetilen DNS sunucuları cloudapp.azure.com toohello ortak IP adresi. Örneğin, genel IP kaynağı ile oluşturursanız, **contoso** olarak bir *domainnamelabel* hello içinde **Batı ABD** Azure *konumu*, hello tam etki alanı adı (FQDN) **contoso.westus.cloudapp.azure.com** toohello genel IP adresi hello kaynağının çözer. Bu FQDN toocreate Azure'da toohello genel IP adresine işaret eden bir özel etki alanı CNAME kaydı kullanabilirsiniz.

> [!IMPORTANT]
> Oluşturulan her bir etki alanı ad etiketi kendi Azure konumunda benzersiz olmalıdır.  
>

### <a name="virtual-machines"></a>Sanal makineler
Bir ortak IP adresi ile ilişkilendirebilirsiniz bir [Windows](../virtual-machines/windows/overview.md) veya [Linux](../virtual-machines/virtual-machines-linux-about.md) tooits atayarak VM **ağ arabirimi**. Birden çok ağ arabirimlerine sahip bir VM Hello durumda bunu toohello atayabilirsiniz *birincil* yalnızca ağ arabirimi. Dinamik veya bir statik genel IP adresi tooa VM atayabilirsiniz.

### <a name="internet-facing-load-balancers"></a>İnternet'e yönelik yük dengeleyiciler
Bir ortak IP adresi ile ilişkilendirebilirsiniz bir [Azure yük dengeleyici](../load-balancer/load-balancer-overview.md), yük dengeleyici toohello atayarak **ön uç** yapılandırma. Bu genel IP adresi yükü dengelenmiş bir sanal IP adresi (VIP) olarak işlev görür. Dinamik veya statik genel IP adresi tooa yük dengeleyici ön uç atayabilirsiniz. Sağlayan birden çok ortak IP adresleri tooa yük dengeleyici ön uç, ayrıca atayabilirsiniz [çoklu VIP](../load-balancer/load-balancer-multivip.md) senaryoları çok kiracılı ortamı SSL tabanlı Web sitelerinde ister.

### <a name="vpn-gateways"></a>VPN ağ geçitleri
[Azure VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md) kullanılan tooconnect bir Azure sanal ağı (VNet) tooother Azure Vnet veya tooan şirket içi bir ağdır. Tooassign bir ortak IP adresi tooits gerek **IP yapılandırması** tooenable, toocommunicate hello uzak ağ ile. Şu anda yalnızca atayabilirsiniz bir *dinamik* ortak IP adresi tooa VPN ağ geçidi.

### <a name="application-gateways"></a>Uygulama ağ geçitleri
Bir ortak IP adresi ile Azure ilişkilendirebilirsiniz [uygulama ağ geçidi](../application-gateway/application-gateway-introduction.md), toohello ağ geçidi atayarak **ön uç** yapılandırma. Bu genel IP adresi yükü dengelenmiş bir VIP olarak işlev görür. Şu anda yalnızca atayabilirsiniz bir *dinamik* ortak IP adresi tooan uygulama ağ geçidi ön uç yapılandırması.

### <a name="at-a-glance"></a>Bir bakışta
Merhaba tabloda bir ortak IP adresi olabilen hello belirli özellik ilişkili tooa en üst düzey kaynak ve kullanılabilecek hello ayırma yöntemlerini (dinamik veya statik) gösterir.

| En üst düzey kaynak | IP Adresi ilişkilendirme | Dinamik | Statik |
| --- | --- | --- | --- |
| Sanal makine |Ağ arabirimi |Evet |Evet |
| Yük dengeleyici |Ön uç yapılandırması |Evet |Evet |
| VPN ağ geçidi |Ağ geçidi IP yapılandırması |Evet |Hayır |
| Uygulama ağ geçidi |Ön uç yapılandırması |Evet |Hayır |

## <a name="private-ip-addresses"></a>Özel IP adresleri
Özel IP adreslerinin izin diğer kaynaklarla Azure kaynaklarını toocommunicate bir [sanal ağ](virtual-networks-overview.md) veya bir VPN ağ geçidi veya Internet erişilebilir IP adresi kullanmadan expressroute bağlantı hattı üzerinden şirket içi ağ.

Hello Azure Resource Manager dağıtım modelinde, Azure kaynak türleri aşağıdaki ilişkili toohello özel bir IP adresi şöyledir:

* VM'ler
* İç yük dengeleyiciler (ILB)
* Uygulama ağ geçitleri

### <a name="allocation-method"></a>Ayırma yöntemi
Özel bir IP adresi ayrılmış hello adresinden hello alt toowhich hello kaynağın aralığı eklenir. Merhaba alt kendisini Hello adres aralığı hello sanal ağınızın adres aralığı bir parçasıdır.

Özel IP adresi ayırmak için kullanılan iki yöntem vardır: *Dinamik* veya *statik*. Merhaba varsayılan ayırma yöntemi *dinamik*, burada başlangıç IP adresi (DHCP kullanarak) hello kaynağın alt ağından otomatik olarak ayrılır. Bu IP adresi, durdurmak ve hello kaynak başlatmak değiştirebilirsiniz.

Merhaba ayırma yöntemi çok ayarlayabilirsiniz*statik* aynı hello tooensure başlangıç IP adresi kalır. Bu durumda, ayrıca tooprovide hello kaynağın alt ağının parçası olan geçerli bir IP adresi gerekir.

Statik özel IP adresleri yaygın olarak şunlar için kullanılır:

* Etki alanı denetleyicisi veya DNS sunucusu olarak çalışan VM’ler.
* IP adreslerini kullanan güvenlik duvarı kuralları gerektiren kaynaklar.
* Bir IP adresi üzerinden diğer uygulamalar/kaynaklar tarafından erişilen kaynaklar.

### <a name="virtual-machines"></a>Sanal makineler
Özel bir IP adresi toohello atanmış **ağ arabirimi** , bir [Windows](../virtual-machines/windows/overview.md) veya [Linux](../virtual-machines/virtual-machines-linux-about.md) VM. Bir VM’nin birden çok ağ arabirimi olması durumunda her arabirime özel bir IP adresi atanır. Merhaba ayırma yöntemi dinamik ya da bir ağ arabirimi için statik olarak belirtebilirsiniz.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>İç DNS ana bilgisayar adı çözümlemesi (VM’ler için)
Siz açıkça özel DNS sunucuları yapılandırmadığınız sürece, tüm Azure VM’leri varsayılan olarak [Azure tarafından yönetilen DNS sunucuları](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) ile yapılandırılmıştır. Bu DNS sunucuları aynı hello içinde bulunan VM'ler için dahili ad çözümlemesi sağlamak VNet.

Bir VM oluştururken hello hostname tooits özel IP adresi için bir eşleme toohello Azure tarafından yönetilen DNS sunucuları eklenir. Bir çok ağ arabirimine VM durumunda hello hostname eşlendi hello birincil ağ arabirimi toohello özel IP adresi.

VM Azure tarafından yönetilen DNS sunucuları ile yapılandırılmış VNet tootheir özel IP adresleri içindeki tüm VM'lerin mümkün tooresolve hello ana bilgisayar adı olacaktır.

### <a name="internal-load-balancers-ilb--application-gateways"></a>İç yük dengeleyiciler (ILB) ve Uygulama ağ geçitleri
Özel bir IP adresi toohello atayabilirsiniz **ön uç** yapılandırmasını bir [Azure iç yük dengeleyici](../load-balancer/load-balancer-internal-overview.md) (ILB) veya bir [Azure uygulama ağ geçidi](../application-gateway/application-gateway-introduction.md). Bu özel bir IP adresi iç uç noktası olarak hizmet veren, sanal ağ (VNet) ve hello uzak ağlar içinde erişilebilir yalnızca toohello kaynakları toohello VNet bağlanır. Ya da bir dinamik veya statik özel IP adresi toohello ön uç yapılandırması atayabilirsiniz.

### <a name="at-a-glance"></a>Bir bakışta
Merhaba tabloda özel bir IP adresi olabilen hello belirli özellik ilişkili tooa en üst düzey kaynak ve kullanılabilecek hello ayırma yöntemlerini (dinamik veya statik) gösterir.

| En üst düzey kaynak | IP adresi ilişkilendirme | Dinamik | Statik |
| --- | --- | --- | --- |
| Sanal makine |Ağ arabirimi |Evet |Evet |
| Yük dengeleyici |Ön uç yapılandırması |Evet |Evet |
| Uygulama ağ geçidi |Ön uç yapılandırması |Evet |Evet |

## <a name="limits"></a>Sınırlar
Merhaba sınır IP adresleme uygulanmaz hello tam kümesi içinde belirtilen [sınırlar için ağ](../azure-subscription-service-limits.md#networking-limits) azure'da. Bu kısıtlamalar bölge ve abonelik başınadır. Yapabilecekleriniz [desteğine başvurun](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooincrease hello varsayılan sınırları iş gereksinimlerinize göre toohello maksimum sınırlarını ayarlama.

## <a name="pricing"></a>Fiyatlandırma
Genel IP adreslerinin nominal bir ücreti olabilir. toolearn IP hakkında daha fazla adres Azure, gözden geçirme hello fiyatlandırma [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası.

## <a name="next-steps"></a>Sonraki adımlar
* [Bir VM hello Azure portal kullanarak bir statik genel IP ile dağıtma](virtual-network-deploy-static-pip-arm-portal.md)
* [Şablon kullanarak statik genel IP’li VM dağıtma](virtual-network-deploy-static-pip-arm-template.md)
* [Bir VM hello Azure portal kullanarak statik özel bir IP adresi ile dağıtma](virtual-networks-static-private-ip-arm-pportal.md)
