---
title: "Premium Azure Redis önbelleği için bir sanal ağ aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl toocreate ve Premium katmanı Azure Redis önbelleği örnekleri için sanal ağ desteğini yönetme"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>Sanal ağ tooconfigure destek nasıl Premium Azure Redis önbelleği için
Azure Redis önbelleği önbellek boyutu ve özelliklerin Premium katmanı özellikleri kümeleme, sürdürme ve sanal ağ desteği gibi hello seçimi esneklik sağlayan farklı önbellek teklifleri vardır. Bir VNet hello bulutta özel bir ağdır. Bir Azure Redis önbelleği örneğine sahip bir VNet yapılandırıldığında, genel olarak adreslenebilir değildir ve yalnızca sanal makineler ve uygulamalardan hello VNet içinde erişilebilir. Bu makalede nasıl tooconfigure sanal ağı desteklemek için bir premium Azure Redis önbelleği örneği açıklanmaktadır.

> [!NOTE]
> Azure Redis önbelleği destekleyen her iki Klasik ve Resource Manager sanal ağlar.
> 
> 

Diğer premium önbellek özellikleri hakkında daha fazla bilgi için bkz: [giriş toohello Azure Redis önbelleği Premium katmanına](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>Neden VNet?
[Azure sanal ağı (VNet)](https://azure.microsoft.com/services/virtual-network/) Gelişmiş Güvenlik ve yalıtım, Azure Redis önbelleği yanı sıra alt ağlar, erişim denetimi ilkeleri için dağıtım sağlar ve diğer özellikleri toofurther erişimi kısıtlayın.

## <a name="virtual-network-support"></a>Sanal ağ desteği
Sanal ağ (VNet) desteği üzerinde hello yapılandırılmış **yeni Redis önbelleği** dikey önbellek oluşturma sırasında. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Premium fiyatlandırma katmanına seçtikten sonra hello olan bir VNet seçerek Redis VNet tümleştirme yapılandırabilirsiniz aynı abonelikte ve konumda önbelleğiniz olarak. toouse yeni bir VNet oluşturun ilk hello adımları izleyerek [hello Azure portal kullanarak bir sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) veya [hello Azure portal kullanarak bir sanal ağ (Klasik) oluşturmak](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) ve toohello döndürür **Yeni Redis önbelleği** dikey toocreate ve premium önbelleğiniz yapılandırın.

Yeni önbelleğiniz için tooconfigure hello VNet tıklatın **sanal ağ** hello üzerinde **yeni Redis önbelleği** dikey penceresinde ve select hello hello aşağı açılan listeden VNet istenen.

![Sanal ağ][redis-cache-vnet]

Select hello istenen alt ağ hello üzerinden **alt** aşağı açılan listesinde ve istenen hello belirtin **statik IP adresi**. Klasik bir VNet hello kullanıyorsanız **statik IP adresi** alan isteğe bağlıdır ve belirtilmemişse, biri seçili hello alt ağdan seçilir.

> [!IMPORTANT]
> Azure Redis önbelleği tooa Resource Manager Vnet'i dağıtırken hello önbellek Azure Redis önbelleği örnekleri dışında başka kaynaklar içeren özel bir alt ağda olmalıdır. Azure Redis önbelleği tooa içeren diğer kaynaklar, hello dağıtım Resource Manager Vnet'i tooa alt girişimde toodeploy başarısız olur.
> 
> 

![Sanal ağ][redis-cache-vnet-ip]

> [!IMPORTANT]
> Her alt ağ içindeki bazı IP adreslerini Azure ayırır ve bu adresleri kullanılamaz. Merhaba ilk ve son IP adresleri hello alt Azure Hizmetleri için kullanılan üç daha fazla adres birlikte Protokolü uyum için ayrılmıştır. Daha fazla bilgi için bkz: [bu alt ağ içindeki IP adresleri kullanma kısıtlamaları vardır?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> Hello Azure sanal ağ altyapısı tarafından kullanılan ek toohello IP adresleri, her Redis örnek parça her hello alt ağ kullanan iki IP adresi ve hello yük dengeleyici için bir ek IP adresi. Kümelenmemiş bir önbellek toohave bir parça olarak kabul edilir.
> 
> 

Merhaba önbellek oluşturulduktan sonra tıklayarak hello VNet hello yapılandırmasını görüntüleyebilirsiniz **sanal ağ** hello gelen **kaynak menü**.

![Sanal ağ][redis-cache-vnet-info]

bir sanal ağ kullanırken tooconnect tooyour Azure Redis önbelleği örneği hello ana bilgisayar adını belirtin önbelleğiniz hello bağlantı dizesinde hello aşağıdaki örnekte gösterildiği gibi:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Azure Redis önbelleği sanal ağ ile ilgili SSS
liste aşağıdaki hello hello Azure Redis önbelleği ölçeklendirme hakkında sorular yanıtlar toocommonly içerir.

* [Azure Redis önbelleği ve Vnet ile ilgili bazı ortak yetersizliğini sorunları nelerdir?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [My önbelleği sanal ağ içinde çalıştığını nasıl doğrulayabilirsiniz?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [Sanal ağlar ile standart ya da temel bir önbellek kullanabilir miyim?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [Neden Redis önbelleği oluşturma bazı alt ağların ancak diğer başarısız oluyor?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Merhaba alt ağ adres alanı gereksinimleri nelerdir?](#what-are-the-subnet-address-space-requirements)
* [Tüm önbellek özellikleri, bir VNET önbelleğinde barındırdığında çalışıyor mu?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Azure Redis önbelleği ve Vnet ile ilgili bazı ortak yetersizliğini sorunları nelerdir?
Azure Redis önbelleği sanal ağ içinde barındırıldığında, tablolar aşağıdaki hello hello bağlantı noktaları kullanılır. 

>[!IMPORTANT]
>Tabloları aşağıdaki hello Hello bağlantı noktaları engellenirse hello önbellek düzgün çalışmayabilir. Bir veya daha fazla engellenen Bu bağlantı noktalarına sahip hello en yaygın yetersizliğini Azure Redis Önbelleği'nde bir sanal ağ kullanırken bir sorundur.
> 
> 

- [Giden bağlantı noktası gereksinimleri](#outbound-port-requirements)
- [Gelen bağlantı noktası gereksinimleri](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Giden bağlantı noktası gereksinimleri

Yedi giden bağlantı noktası gereksinimleri vardır.

- İsterseniz, internet üzerinden bir istemciye ait yapılabilmesi için tüm giden bağlantılar toohello denetim cihaz şirket içi.
- Üç hello bağlantı noktalarının Azure Storage ve Azure DNS hizmeti trafiğini tooAzure uç noktaları rota.
- bağlantı noktası aralıkları kalan hello ve iç Redis alt ağ iletişimleri için. Hiçbir alt ağ NSG kuralları iç Redis alt ağ iletişimleri için gerekli değildir.

| Bağlantı noktaları | Yön | Aktarım Protokolü | Amaç | Yerel IP | Uzak IP |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |Giden |TCP |Bağımlılıklar üzerinde Azure depolama/PKI (Internet) redis | (Alt ağ redis) |* |
| 53 |Giden |TCP/UDP |DNS (Internet/VNet) bağımlılıkları redis | (Alt ağ redis) |* |
| 8443 |Giden |TCP |Redis iç iletişiminde | (Alt ağ redis) | (Alt ağ redis) |
| 10221-10231 |Giden |TCP |Redis iç iletişiminde | (Alt ağ redis) | (Alt ağ redis) |
| 20226 |Giden |TCP |Redis iç iletişiminde | (Alt ağ redis) |(Alt ağ redis) |
| 13000-13999 |Giden |TCP |Redis iç iletişiminde | (Alt ağ redis) |(Alt ağ redis) |
| 15000-15999 |Giden |TCP |Redis iç iletişiminde | (Alt ağ redis) |(Alt ağ redis) |


### <a name="inbound-port-requirements"></a>Gelen bağlantı noktası gereksinimleri

Sekiz gelen bağlantı noktası aralığı gereksinimi yoktur. Bu aralıklardaki gelen istekleri olan ya da hello barındırılan diğer hizmetlerden gelen aynı sanal ağ veya iç toohello Redis alt ağ iletişimleri.

| Bağlantı noktaları | Yön | Aktarım Protokolü | Amaç | Yerel IP | Uzak IP |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |Gelen |TCP |İstemci iletişimi tooRedis, Azure Yük Dengeleme | (Alt ağ redis) |Sanal ağ, Azure yük dengeleyici |
| 8443 |Gelen |TCP |Redis iç iletişiminde | (Alt ağ redis) |(Alt ağ redis) |
| 8500 |Gelen |TCP/UDP |Azure Yük Dengeleme | (Alt ağ redis) |Azure Load Balancer |
| 10221-10231 |Gelen |TCP |Redis iç iletişiminde | (Alt ağ redis) |(Redis. alt ağ), Azure yük dengeleyici |
| 13000-13999 |Gelen |TCP |İstemci iletişimi tooRedis kümeleri, Azure Yük Dengeleme | (Alt ağ redis) |Sanal ağ, Azure yük dengeleyici |
| 15000-15999 |Gelen |TCP |İstemci iletişimi tooRedis kümeleri, Azure Yük Dengeleme | (Alt ağ redis) |Sanal ağ, Azure yük dengeleyici |
| 16001 |Gelen |TCP/UDP |Azure Yük Dengeleme | (Alt ağ redis) |Azure Load Balancer |
| 20226 |Gelen |TCP |Redis iç iletişiminde | (Alt ağ redis) |(Alt ağ redis) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Ek sanal ağ bağlantı gereksinimleri

Azure Redis önbelleği sanal bir ağa başlangıçta karşılanır değil için ağ bağlantı gereksinimleri vardır. Azure Redis önbelleği tüm düzgün bir şekilde bir sanal ağ içindeki kullanıldığında öğeleri toofunction aşağıdaki hello gerektirir.

* Giden ağ bağlantısı tooAzure depolama uç noktaları dünya çapında. Bu uç noktaları hello bulunan içerir bulunan depolama uç noktaları yanı sıra hello Azure Redis önbelleği örneği aynı bölgede **diğer** Azure bölgeleri. Azure depolama uç noktaları çözmek DNS etki alanı aşağıdaki hello altında: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net*ve *file.core.windows.net*. 
* Giden çok ağ bağlantısı*ocsp.msocsp.com*, *mscrl.microsoft.com*, ve *crl.microsoft.com*. Bu bağlantı, gerekli toosupport SSL işlevdir.
* Merhaba hello sanal ağ için DNS yapılandırmasını hello bitiş noktalarının tümü çözme yeteneğine sahip olmalı ve etki alanları belirtilen hello önceki noktaları. Geçerli bir DNS altyapısının yapılandırılmış ve sanal ağ için hello saklanır sağlayarak bu DNS gereksinimleri karşılanabilir.
* DNS etki alanı aşağıdaki hello altında çözmek Azure Monitoring uç aşağıdaki giden ağ bağlantısı toohello: shoebox2 black.shoebox2.metrics.nsatc.net, Kuzey-prod2.prod2.metrics.nsatc.net azglobal-black.azglobal.metrics.nsatc.net, shoebox2-red.shoebox2.metrics.nsatc.net, Doğu-prod2.prod2.metrics.nsatc.net azglobal-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>My önbelleği sanal ağ içinde çalıştığını nasıl doğrulayabilirsiniz?

>[!IMPORTANT]
>Sanal ağ içinde barındırılan tooan Azure Redis önbelleği örneğine bağlanırken, istemciler olmalıdır önbelleğiniz herhangi bir sınama uygulamalarını veya tanılama ping araçları dahil olmak üzere aynı sanal hello.
>
>

Başlangıç bağlantı noktası gereksinimleri hello önceki bölümde açıklandığı gibi yapılandırıldıktan sonra önbelleğiniz hello aşağıdaki adımları gerçekleştirerek çalışıp çalışmadığını doğrulayabilirsiniz.

- [Yeniden başlatma](cache-administration.md#reboot) tüm hello önbelleğe düğümleri. Tüm hello önbellek bağımlılıkları ulaşılamıyor gerekirse (açıklandığı gibi [gelen bağlantı noktası gereksinimleri](cache-how-to-premium-vnet.md#inbound-port-requirements) ve [giden bağlantı noktası gereksinimleri](cache-how-to-premium-vnet.md#outbound-port-requirements)), hello önbellek olmayacak mümkün toorestart başarıyla.
- Merhaba önbellek düğümleri (Merhaba önbellek durumu hello Azure portal tarafından belirlendiği şekilde) yeniden başlattıktan sonra testleri aşağıdaki hello gerçekleştirebilirsiniz:
  - (bağlantı noktası 6380 kullanarak) hello önbellek son nokta hello içinde olan bir makineden ping hello olarak aynı sanal ağ kullanılarak önbelleğe [tcping](https://www.elifulkerson.com/projects/tcping.php). Örneğin:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Merhaba, `tcping` aracı raporları hello bağlantı açıksa, hello önbellek hello VNET istemcilerinden gelen bağlantı için kullanılabilir.

  - Toocreate test önbellek istemcisi başka bir şekilde tootest olduğu (basit bir olabilir StackExchange.Redis kullanarak konsol uygulaması) toohello önbellek bağlanır ve ekler ve bazı öğeler hello önbellekten alır. Merhaba örnek istemci uygulaması olan bir VM üzerine yükleme hello önbelleği olarak aynı sanal ağı hello ve tooverify bağlantı toohello önbellek çalıştırın.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>Sanal ağlar ile standart ya da temel bir önbellek kullanabilir miyim?
Sanal ağlar yalnızca premium önbelleklere ile kullanılabilir.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>Neden Redis önbelleği oluşturma bazı alt ağların ancak diğer başarısız oluyor?
Azure Redis önbelleği tooa Resource Manager Vnet'i dağıtıyorsanız, hello önbelleği başka bir kaynak türünü içeren özel bir alt ağda olmalıdır. Azure Redis önbelleği tooa içeren diğer kaynaklar, hello dağıtım Resource Manager Vnet'i alt girişimde toodeploy başarısız olur. Yeni Redis önbelleği oluşturabilmeniz için önce hello alt ağ içindeki hello mevcut kaynakların silmeniz gerekir.

Birden çok tür dağıtabilirsiniz yeterli IP olduğu sürece kaynakları tooa Klasik VNet kullanılabilir giderir.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Merhaba alt ağ adres alanı gereksinimleri nelerdir?
Her alt ağ içindeki bazı IP adreslerini Azure ayırır ve bu adresleri kullanılamaz. Merhaba ilk ve son IP adresleri hello alt Azure Hizmetleri için kullanılan üç daha fazla adres birlikte Protokolü uyum için ayrılmıştır. Daha fazla bilgi için bkz: [bu alt ağ içindeki IP adresleri kullanma kısıtlamaları vardır?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

Hello Azure sanal ağ altyapısı tarafından kullanılan ek toohello IP adresleri, her Redis örnek parça her hello alt ağ kullanan iki IP adresi ve hello yük dengeleyici için bir ek IP adresi. Kümelenmemiş bir önbellek toohave bir parça olarak kabul edilir.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>Tüm önbellek özellikleri, bir VNET önbelleğinde barındırdığında çalışıyor mu?
Önbelleğinizi VNET parçası olduğunda, yalnızca hello VNET istemcilerinde hello önbelleğe erişebilir. Sonuç olarak, hello aşağıdaki önbellek yönetim özellikleri şu anda çalışmıyor.

* Konsol redis - VNET hello dışında olan yerel tarayıcınızda Redis Konsolu çalıştıran tooyour önbellek bağlanılamıyor.

## <a name="use-expressroute-with-azure-redis-cache"></a>ExpressRoute ile Azure Redis önbelleğini kullanma
Müşteriler bağlanabileceği bir [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) hattı tootheir sanal ağ altyapısı, böylece kendi şirket içi ağ tooAzure genişletme. 

Varsayılan olarak, yeni oluşturulan bir expressroute bağlantı hattı zorlamalı tünel gerçekleştirmez (varsayılan yol tanıtım 0.0.0.0/0) bir VNET üzerinde. Sonuç olarak, doğrudan hello VNET ' giden Internet bağlantısına izin verilen ve istemci uygulamalardır mümkün tooconnect tooother Azure uç noktaları Azure Redis önbelleği dahil olmak üzere.

Ancak bir ortak müşteri zorlanan tünel toouse yapılandırmasıdır (varsayılan rota tanıtma) giden Internet trafiği tooinstead akış içi zorlar. Bu trafik akışı hello giden trafiği ise, Azure Redis önbelleği ile bağlantısını keser. ardından hello Azure Redis önbelleği örneği mümkün toocommunicate bağımlılıklarını ile değil, şirket içi engellendi.

Merhaba, toodefine bir (veya daha fazla) kullanıcı tanımlı yollar (Udr'ler) hello Azure Redis önbelleği içeren hello alt ağdaki çözümüdür. Bir UDR hello varsayılan yol yerine uyulacaktır alt özel yollar tanımlar.

Mümkünse, bu yapılandırma aşağıdaki toouse hello önerilir:

* Merhaba ExpressRoute yapılandırma 0.0.0.0/0 tanıtır ve varsayılan olarak tüm giden trafiği şirket içi zorlamalı tünel oluşturur.
* Merhaba hello Azure Redis önbelleği içeren uygulanan UDR toohello alt tanımlar 0.0.0.0/0 TCP/IP'yi trafiği toohello için bir çalışma rota ile ortak Internet; Örneğin ayarı hello tarafından türü too'Internet sonraki atlama '.

Merhaba birleşik bu adımları hello alt düzey UDR hello zorlanan tünel, ExpressRoute böylece hello Azure Redis önbelleği giden Internet erişim sağlamaya göre öncelik kazanır etkisidir.

ExpressRoute kullanarak şirket içi uygulama bağlanan tooan Azure Redis önbelleği örneği tipik kullanım senaryosu tooperformance nedenlerden dolayı değil (Azure Redis önbelleği en iyi performans için istemcileri hello olmalıdır hello Azure Redis önbelleği ile aynı bölgeye).

>[!IMPORTANT] 
>Merhaba UDR içinde tanımlanan yollar **gerekir** hello ExpressRoute yapılandırma tarafından tanıtılan rotaları üzerinden yeterince spesifik tootake öncelik olması. Merhaba aşağıdaki örnek hello geniş 0.0.0.0/0 adres aralığını kullanır ve bu nedenle olası yanlışlıkla daha belirli adres aralıkları kullanarak Yol tanıtımlarını tarafından geçersiz kılınabilir.

>[!WARNING]  
>Azure Redis önbelleği ile ExpressRoute yapılandırmaları desteklenmez, **yanlış cross-hello ortak eşleme yolu toohello özel eşleme yolu yolları tanıtma**. Yapılandırılmış, ortak eşleme sahip ExpressRoute yapılandırmaları çok sayıda Microsoft Azure IP adres aralıkları için Microsoft'tan Yol tanıtımlarını alırsınız. Bu adres aralıklarını yanlış cross-hello özel eşleme yoluna tanıtılan varsa, hello sonuç tüm giden ağ paketlerinin hello Azure Redis önbelleği örneğinin alt ağdan hatalı zorlamalı tünel tooa müşterinin şirket içi ağ olmasıdır Altyapı. Bu ağ akışı Azure Redis önbelleği keser. Merhaba ortak eşleme yolu toohello özel eşleme yolu toostop arası reklam yolları Hello çözüm toothis sorunudur.


Kullanıcı tanımlı yollar hakkında arka plan bilgileri kullanılabilir bu [genel bakış](../virtual-network/virtual-networks-udr-overview.md).

ExpressRoute hakkında daha fazla bilgi için bkz: [ExpressRoute teknik genel bakış](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Sonraki adımlar
Toouse daha premium özellikleri nasıl önbelleğe alma hakkında bilgi edinin.

* [Giriş toohello Azure Redis önbelleği Premium katmanına](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

