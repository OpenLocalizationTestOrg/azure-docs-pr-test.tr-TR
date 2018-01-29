---
title: "Azure sanal ağ hizmet uç noktaları | Microsoft Docs"
description: "Hizmet uç noktalarını kullanarak bir sanal ağdan Azure kaynaklarına doğrudan erişimi etkinleştirmeyi öğrenin."
services: virtual-network
documentationcenter: na
author: anithaa
manager: narayan
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/15/2017
ms.author: anithaa
ms.custom: 
ms.openlocfilehash: 7b5675dacd1d9effd73f3bc51ea4efc0ea6be029
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/20/2017
---
# <a name="virtual-network-service-endpoints-preview"></a>Sanal Ağ Hizmet Uç Noktaları (Önizleme)

Sanal Ağ hizmet uç noktaları, sanal ağ özel adres alanınızı ve sanal ağınızın kimliğini doğrudan bağlantı üzerinden Azure hizmetlerine genişletir. Uç noktalar kritik Azure hizmeti kaynaklarınızı sanal ağlarınızla sınırlayarak güvenliğini sağlamanıza imkan verir. Sanal ağınızdan Azure hizmetine giden trafik her zaman Microsoft Azure omurga ağında kalır.

Bu özellik aşağıdaki Azure hizmetleri ve bölgeleri için önizleme sürümündedir:

- **Azure Depolama**: Azure genel bulutundaki tüm bölgeler.
- **Azure SQL**: Azure genel bulutundaki tüm bölgeler.

En güncel önizleme bildirimleri için [Azure Sanal Ağ güncelleştirmeleri](https://azure.microsoft.com/updates/?product=virtual-network) sayfasını inceleyin.

>[!NOTE]
> Önizleme sırasında bu özellik genel kullanılabilirlik sunumundaki özelliklerle aynı seviyede kullanılabilirliğe ve güvenilirliğe sahip olmayabilir. Daha fazla bilgi için bkz. [Microsoft Azure Önizlemeleri için Microsoft Azure Ek Kullanım Koşulları](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="key-benefits"></a>Önemli avantajlar

Hizmet uç noktaları aşağıdaki avantajları sağlar:

- **Azure hizmet kaynaklarınız için geliştirilmiş güvenlik**: Hizmet uç noktaları sayesinde, Azure hizmet kaynakları sanal ağınızla sınırlandırılarak güvenli hale getirilebilir. Hizmet kaynaklarını bir sanal ağ ile sınırlandırmak, ilgili kaynaklara genel İnternet erişimini tamamen kaldırıp yalnızca sanal ağınızdan gelen trafiğe izin vererek güvenliği artırır.
- **Sanal Ağınızdan gelen Azure trafiği için en uygun yönlendirme**: Günümüzde sanal ağınızda İnternet trafiğini şirket içi ve/veya sanal gereçlerden geçmeye zorlayan tüm rotalar (zorlamalı tünel oluşturma olarak bilinir) Azure hizmet trafiğini de İnternet trafiğiyle aynı rotadan geçmeye zorlar. Hizmet uç noktaları Azure trafiği için en uygun rotayı sunar. 

  Uç noktalar her zaman hizmet trafiğini sanal ağınızdan doğrudan Microsoft Azure omurga ağındaki hizmete yönlendirir. Trafiğin Azure omurga ağında tutulması, zorlamalı tünel aracılığıyla hizmet trafiğini etkilemeden, giden İnternet trafiğini sanal ağlarınızdan denetlemeye ve izlemeye devam etmenize olanak sağlar. [Kullanıcı tanımlı rotalar ve zorlamalı tünel oluşturma](virtual-networks-udr-overview.md) hakkında daha fazla bilgi edinin.
- **Kolay kurulum sayesinde daha az yönetim yükü**: Azure kaynaklarını IP güvenlik duvarı aracılığıyla güvenli hale getirmek için artık sanal ağınızda ayrılmış, ortak IP adresleri olması gerekmez. Hizmet uç noktalarını ayarlamak için herhangi bir NAT veya ağ geçidi cihazı gerekmez. Hizmet uç noktaları alt ağda tek tıklamayla yapılandırılabilir. Uç noktaların bakımını yapma yükü ortadan kalkar.

## <a name="limitations"></a>Sınırlamalar

- Bu özellik yalnızca Azure Resource Manager dağıtım modeli üzerinden dağıtılmış olan sanal ağlarda kullanılabilir.
- Uç noktalar Azure sanal ağlarında yapılandırılmış olan alt ağlarda etkindir. Uç noktalar şirket içi ortamdan Azure hizmetlerine giden trafik için kullanılamaz. Daha fazla bilgi için bkz. [Azure hizmetine erişimi şirket içi ortamla sınırlama](#securing-azure-services-to-virtual-networks).
- Hizmet uç noktası yalnızca sanal ağ ile aynı bölgedeki Azure hizmeti trafiği için geçerlidir. Azure Depolama hizmetinde RA-GRS ve GRS trafiğinin desteklenmesi için özelliğin kapsamı sanal ağın dağıtılmış olduğu eşleştirilmiş bölgeye uzatılır. [Azure eşleştirilmiş bölgeleri](../best-practices-availability-paired-regions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-paired-regions) hakkında daha fazla bilgi edinin.

## <a name="securing-azure-services-to-virtual-networks"></a>Azure hizmetlerini sanal ağlar ile sınırlama

- Sanal ağ hizmet uç noktası, Azure hizmetine sanal ağınızın kimliğini sağlar. Hizmet uç noktaları sanal ağınızda etkinleştirdikten sonra, kaynaklara bir sanal ağ kuralı ekleyerek sanal ağınıza bağlı olan Azure hizmet kaynaklarının güvenliğini sağlayabilirsiniz.
- Günümüzde, bir sanal ağdan gelen Azure hizmet trafiği, kaynak IP adresleri olarak ortak IP adreslerini kullanır. Hizmet uç noktaları ile, hizmet trafiği sanal ağınızdan Azure hizmetinize erişim sırasında kaynak IP adresleri olarak sanal ağ özel adreslerini kullanır. Bu anahtar IP güvenlik duvarlarında kullanılan ayrılmış ve genel IP adreslerini kullanmadan hizmetlere erişmenizi sağlar.
- __Azure hizmetine erişimi şirket içi ortamla sınırlama__:

  Varsayılan olarak sanal ağlara ayrılmış olan Azure hizmeti kaynaklarına şirket içi ağlardan erişmek mümkün değildir. Şirket içinden gelen trafiğe izin vermek istiyorsanız şirket içi ortamdan veya ExpressRoute üzerinden genel (genelde NAT) IP adreslerine de izin vermeniz gerekir. Azure hizmet kaynakları için bu IP adresleri IP güvenlik duvarı yapılandırma adımından eklenebilir.

  ExpressRoute: Ortak eşleme veya Microsoft eşlemesi için şirket içinden [ExpressRoute](../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) kullanıyorsanız, kullanılan NAT IP adreslerini tanımlamanız gerekir. Ortak eşleme için, her bir ExpressRoute varsayılan olarak bağlantı hattında trafik Microsoft Azure omurga ağına girdiğinde Azure hizmet trafiğine uygulanan iki NAT IP adresi kullanılır. Microsoft eşlemesi için, kullanılan NAT IP adresleri müşteri tarafından sağlanır veya hizmet sağlayıcısı tarafından sağlanır. Hizmet kaynaklarınıza erişime izin vermek için, bu genel IP adreslerine kaynak IP güvenlik duvarı ayarında izin vermeniz gerekir. Ortak eşleme ExpressRoute bağlantı hattı IP adreslerinizi bulmak için Azure portalında [ExpressRoute ile bir destek bileti açın](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview). [ExpressRoute genel ve Microsoft eşlemesi için NAT](../expressroute/expressroute-nat.md?toc=%2fazure%2fvirtual-network%2ftoc.json#nat-requirements-for-azure-public-peering) hakkında daha fazla bilgi edinin.

![Azure hizmetlerini sanal ağlar ile sınırlama](./media/virtual-network-service-endpoints-overview/VNet_Service_Endpoints_Overview.png)

### <a name="configuration"></a>Yapılandırma

- Hizmet uç noktaları bir sanal ağ içindeki alt ağ üzerinde yapılandırılır. Uç noktalar ilgili alt ağ içinde çalışan tüm işlem örneği türleriyle birlikte çalışabilir.
- Bir alt ağdan belirli bir hizmete tek bir hizmet uç noktası etkinleştirilebilir. Bir alt ağ üzerindeki desteklenen tüm Azure hizmetleri (örneğin Azure Depolama veya Azure SQL Veritabanı) için birden fazla hizmet uç noktası yapılandırabilirsiniz.
- Sanal ağların Azure hizmet kaynağıyla aynı bölgede bulunması gerekir. GRS ve RA-GRS Azure Depolama hesapları kullanılıyorsa, birincil hesap sanal ağ ile aynı bölgede olmalıdır.
- Uç noktanın yapılandırıldığı sanal ağ, Azure hizmet kaynağıyla aynı veya ondan farklı abonelikte olabilir. Uç noktaları ayarlamak ve Azure hizmetlerinin güvenliğini sağlamak için gerekli olan izinler hakkında daha fazla bilgi için [Sağlama](#Provisioning) bölümüne bakın.
- Desteklenen hizmetler için yeni veya mevcut kaynaklar ile sanal ağlar arasındaki güvenliği hizmet uç noktaları kullanarak sağlayabilirsiniz.

### <a name="considerations"></a>Dikkat edilmesi gerekenler

- Bir hizmet uç noktası etkinleştirildikten sonra alt ağdan hizmet ile iletişim kurarken, ilgili alt ağdaki sanal makinelerin kaynak IP adresleri genel IPv4 adreslerinden özel IPv4 adreslerine döner. Hizmete giden mevcut açık TCP bağlantıları bu geçiş sırasında kapatılır. Bir alt ağ için hizmete yönelik hizmet uç noktasını etkinleştirmeden veya devre dışı bırakmadan önce çalışan kritik görev olmadığından emin olun. Ayrıca uygulamalarınızın IP adresi değişikliğinin ardından Azure hizmetlerine otomatik olarak bağlanabildiğinden emin olun.

  IP adresi değişiklikleri yalnızca sanal ağınızdan giden hizmet trafiğini etkiler. Sanal makinelerinize atanmış genel IPv4 adreslerinin gelen/giden trafiği üzerinde herhangi bir etki görülmez. Azure hizmetleri açısından, Azure genel IP adreslerini kullanan mevcut güvenlik duvarı kurallarınız varsa bu kurallar sanal ağ özel adresine geçiş yapıldığında çalışmaz.
- Hizmet uç noktaları kullanıldığında, Azure hizmetlerine yönelik DNS girişleri güncel durumdaki halde kalır ve Azure hizmetine atanmış olan ortak IP adreslerini çözümlemeye devam eder.
- Hizmet uç noktasına sahip ağ güvenlik grupları (NSG):
  - Varsayılan olarak NSG'ler giden İnternet trafiğine ve dolayısıyla sanal ağınızdan Azure hizmetlerine giden trafiğe izin verir. Bu durum hizmet uç noktalarında da aynı şekilde çalışmaya devam eder. 
  - Giden İnternet trafiğinin tümünü reddetmek ve yalnızca belirli Azure hizmetlerine giden trafiğe izin vermek istiyorsanız NSG'lerinizde __"Azure hizmet etiketlerini"__ kullanabilirsiniz. Desteklenen Azure hizmetlerini NSG kurallarında hedef olarak belirtebilir ve her etikete ait IP adreslerinin bakımının Azure tarafından yapılmasını sağlayabilirsiniz. Daha fazla bilgi için bkz. [NSG'ler için Azure Hizmet etiketleri.](https://aka.ms/servicetags) 

### <a name="scenarios"></a>Senaryolar

- **Eşlenmiş, bağlı veya birden çok sanal ağ**: Bir sanal ağ içindeki veya birden fazla sanal ağ üzerinde bulunan birden fazla alt ağdaki Azure hizmetlerinin güvenliğini sağlamak için, her bir alt ağdaki hizmet uç noktasını ayrı ayrı etkinleştirebilir ve bu alt ağlara giden Azure hizmet kaynaklarının güvenliğini sağlayabilirsiniz.
- **Sanal ağdan bir Azure hizmetine giden trafiği filtreleme**: Sanal ağdan bir Azure hizmetine giden trafiği incelemek veya filtrelemek isterseniz, ilgili sanal ağa bir ağ sanal gereci dağıtabilirsiniz. Ardından hizmet uç noktalarını ağ sanal gerecinin dağıtılmış olduğu alt ağa uygulayabilir ve Azure hizmet kaynağını yalnızca bu alt ağ ile sınırlayabilirsiniz. Bu senaryo, Azure hizmet erişimini ağ sanal gereci filtresi kullanarak sanal ağınızdan yalnızca belirli Azure kaynaklarına gidecek şekilde sınırlamak istediğinizde yararlı olabilir. Daha fazla bilgi için bkz. [Ağ sanal gereçleri ile çıkış](/azure/architecture/reference-architectures/dmz/nva-ha#egress-with-layer-7-nvas.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
- **Azure kaynaklarını doğrudan sanal ağlara dağıtılan hizmetler ile sınırlandırma**: Çeşitli Azure hizmetleri doğrudan bir sanal ağdaki belirli alt ağlara dağıtılabilir. Yönetilen hizmet alt ağında bir hizmet uç noktası kurarak Azure hizmet kaynaklarını [yönetilen hizmet](virtual-network-for-azure-services.md) alt ağlarına ayırabilirsiniz.

### <a name="logging-and-troubleshooting"></a>Günlüğe kaydetme ve sorun giderme

Hizmet uç noktaları belirli bir hizmet için yapılandırıldıktan sonra geçerli olan hizmet uç noktasını aşağıdaki şekilde doğrulayabilirsiniz: 
 
- Hizmet tanılamada herhangi bir hizmet isteğinin kaynak IP adresini doğrulama. Hizmet uç noktalarına sahip tüm yeni isteklerin kaynak IP adresi değerinde isteği sanal ağınızdan gönderen istemciye atanmış olan sanal ağ özel IP adresi gösterilir. Uç noktası olmadığında bu adres Azure genel IP adreslerinden biri olur.
- Bir alt ağdaki herhangi bir ağ arabiriminin etkin yollarını görüntüleme. Hizmet yolu:
  - Her hizmetin adres ön eki aralıklarına daha belirli bir varsayılan yolu gösterir
  - nextHopType değeri *VirtualNetworkServiceEndpoint* olarak belirlenmiştir
  - Zorlamalı tünel rotalarıyla kıyaslandığında geçerli hizmete daha doğrudan bir bağlantı belirtir

>[!NOTE]
> Hizmet uç noktası rotaları, Azure hizmeti olarak adres ön eki eşleşmesi için BGP veya UDR rotasını geçersiz kılar. [Geçerli rotalarla sorun giderme](virtual-network-routes-troubleshoot-portal.md#using-effective-routes-to-troubleshoot-vm-traffic-flow) hakkında daha fazla bilgi edinin

## <a name="provisioning"></a>Sağlama

Hizmet uç noktaları, bir sanal ağda yazma erişimine sahip bir kullanıcı tarafından sanal ağlarda birbirinden bağımsız olarak yapılandırılabilir. Azure hizmet kaynaklarını bir sanal ağ ile sınırlamak için kullanıcının eklenen alt ağlarda *Microsoft.Network/JoinServicetoaSubnet* iznine sahip olması gerekir. Bu izin varsayılan olarak yerleşik hizmet yöneticisi rollerinde mevcuttur ve özel roller oluşturularak değiştirilebilir.

[Yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ve [özel rollere](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) belirli izinlerin atanması hakkında daha fazla bilgi edinin.

Sanal ağlar ve Azure hizmet kaynakları aynı ağda veya farklı aboneliklerde olabilir. Sanal ağ ve Azure hizmet kaynaklarının farklı aboneliklerde olması halinde kaynakların önizleme boyunca aynı Active Directory (AD) kiracısı altında olması gerekir. 

## <a name="pricing-and-limits"></a>Fiyatlandırma ve limitler

Hizmet uç noktalarının kullanımından ek ücret alınmaz. Azure hizmetleri (Azure Depolama, Azure SQL Veritabanı) için güncel fiyatlandırma modeli uygulanır.

Bir sanal ağ içinde sınırsız sayıda hizmet uç noktası oluşturulabilir.

Bir Azure hizmet kaynağında (Azure Depolama hesabı gibi), hizmetler kaynağın güvenliğini sağlamak amacıyla kullanılan alt ağ sayısını sınırlandırabilir. Ayrıntılar için [Sonraki adımlar](#next-steps) bölümündeki hizmet belgelerini inceleyin.

## <a name="next-steps"></a>Sonraki adımlar

- [Sanal ağ hizmet uç noktalarını nasıl yapılandıracağınızı](virtual-network-service-endpoints-configure.md) öğrenin
- [Bir Azure Depolama hesabını bir sanal ağ ile nasıl sınırlandıracağınızı](../storage/common/storage-network-security.md?toc=%2fazure%2fvirtual-network%2ftoc.json) öğrenin
- [Bir Azure SQL Veritabanını bir sanal ağ ile nasıl sınırlandıracağınızı](../sql-database/sql-database-vnet-service-endpoint-rule-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) öğrenin
- [Sanal ağlar için Azure hizmet tümleştirmesi](virtual-network-for-azure-services.md) hakkında bilgi edinin
-  Hızlı başlangıç: Bir sanal ağın alt ağında hizmet uç noktası ve bu alt ağda güvenli Azure Depolama hesabı oluşturmak için [Azure resource manager şablonu](https://azure.microsoft.com/en-us/resources/templates/201-vnet-2subnets-service-endpoints-storage-integration).

