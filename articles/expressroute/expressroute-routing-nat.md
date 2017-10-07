---
title: "Azure ExpressRoute için NAT | Microsoft Docs"
description: "Bu sayfada, ExpressRoute devreleri için yönlendirmeyi yapılandırma ve yönetmeye yönelik ayrıntılı gereksinimler verilmektedir."
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>ExpressRoute için NAT

ExpressRoute kullanarak, tooconnect tooMicrosoft bulut hizmetlerine yukarı tooset gerekir ve yönlendirme yönetin. Bazı bağlantı sağlayıcıları yönlendirme ayarlama ve yönetimini yönetilen bir hizmet olarak sunar. Bu hizmetin sunulup varsa, bağlantı sağlayıcısı toosee ile denetleyin. Yoksa, toohello gereksinimlerine uymalıdır. 

Toohello başvuran [devreler ve Yönlendirme etki alanları](expressroute-circuit-peerings.md) hello yönlendirme açıklaması için makalenin toobe gereksinim oturumları toofacilitate Bağlantısı'nda ayarlayın.

> [!NOTE]
> Microsoft, yüksek kullanılabilirlik yapılandırmaları için yönlendirici artıklık protokollerini (örn. HSRP, VRRP) desteklemez. Yüksek kullanılabilirlik için eşlik başına yedek bir BGP oturumları çifti kullanılır.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>Eşlemeler için kullanılan IP adresleri

Tooreserve IP birkaç bloklarını gereken adresleri tooconfigure ağınız ile Microsoft'un Enterprise edge (Msee) yönlendiricileri yönlendirmeyi. Bu bölümde gereksinimlerin listesi sağlar ve bu IP adreslerini nasıl alınan ve kullanılan ilgili hello kurallar açıklanmaktadır.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Azure özel eşleme için kullanılan IP adresleri

Özel IP adresleri veya ortak IP adresleri tooconfigure hello eşlemeleri kullanabilirsiniz. Başlangıç adresi aralığı yolları yapılandırmak için kullanılan adres aralıkları kullanılan toocreate azure'da sanal ağlar ile çakışmaması gerekir. 

* Arabirimleri yönlendirmek için bir /29 alt ağı veya iki /30 alt ağı ayırmanız gerekir.
* Yönlendirme için kullanılan hello alt ağlar özel IP adresleri veya ortak IP adresleri olabilir.
* Merhaba alt hello Microsoft bulutunda kullanılmak hello müşteri tarafından ayrılan hello aralığı ile çakışmaması gerekir.
* Bir /29 alt ağı kullanıldığında iki /30 alt ağına bölünür. 
  * ilk hello/30 alt ağı hello birincil bağlantı için kullanılacak ve ikinci /30 hello alt hello ikincil bağlantı için kullanılır.
  * Her hello /30 alt ağlar için Yönlendiricinizde hello ilk IP adresi hello /30 alt kullanmalısınız. Microsoft bir BGP oturumu yukarı hello /30 alt tooset hello ikinci IP adresini kullanır.
  * Her iki BGP oturumunu da ayarlamanız gerekir bizim [kullanılabilirlik SLA](https://azure.microsoft.com/support/legal/sla/) toobe geçerli.  

#### <a name="example-for-private-peering"></a>Özel eşleme örneği

Toouse a.b.c.d/29 tooset eşliği hello yukarı seçerseniz iki/30 alt bölünür. Merhaba aşağıdaki örnekte, hello a.b.c.d/29 alt ağının nasıl kullanıldığına bakılacaktır. 

a.b.c.d/29 bölünmüş tooa.b.c.d/30 ve a.b.c.d+4/30 olacaktır ve API'leri sağlama hello aracılığıyla tooMicrosoft aşağı geçirildi. Merhaba VRF IP'si hello birincil PE'nin ve Microsoft hello VRF IP'si olarak a.b.c.d+2 tüketir için hello gibi birincil MSEE'nin a.b.c.d+1 kullanır. Merhaba VRF IP'si hello ikincil PE'nin ve Microsoft hello VRF IP'si olarak a.b.c.d+6 kullanacağı hello gibi ikincil a.b.c.d+5 kullanır.

Özel eşleme yukarı 192.168.100.128/29 tooset burada seçtiğiniz bir durum düşünün. 192.168.100.128/29 adresi 192.168.100.128 içerir, arasında too192.168.100.135:

* 192.168.100.128/30 toolink1, sağlayıcı 192.168.100.129 ve Microsoft 192.168.100.130 kullanarak ile atanır.
* 192.168.100.132/30 toolink2, sağlayıcı 192.168.100.133 ve Microsoft 192.168.100.134 kullanarak ile atanır.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Azure genel ve Microsoft eşlemesi için kullanılan IP adresleri

Merhaba BGP oturumlarını ayarlamak için sahip olduğunuz ortak IP adreslerini kullanmanız gerekir. Microsoft, mümkün tooverify hello sahipliğini Routing Internet Registries ve Internet Routing Registries aracılığıyla hello IP adresleri olmalıdır. 

* Benzersiz bir kullanmalısınız/29 alt ağı veya iki/30 alt tooset yukarı hello BGP eşliği (birden fazla varsa) her expressroute bağlantı hattı eşliği için. 
* Bir /29 alt ağı kullanıldığında iki /30 alt ağına bölünür. 
  * ilk hello/30 alt ağı hello birincil bağlantı için kullanılacak ve ikinci /30 hello alt hello ikincil bağlantı için kullanılır.
  * Her hello /30 alt ağlar için Yönlendiricinizde hello ilk IP adresi hello /30 alt kullanmalısınız. Microsoft bir BGP oturumu yukarı hello /30 alt tooset hello ikinci IP adresini kullanır.
  * Her iki BGP oturumunu da ayarlamanız gerekir bizim [kullanılabilirlik SLA](https://azure.microsoft.com/support/legal/sla/) toobe geçerli.

## <a name="public-ip-address-requirement"></a>Genel IP adresi gereksinimi

### <a name="private-peering"></a>Özel Eşleme

Özel eşleme için ortak veya özel IPv4 adreslerini toouse seçebilirsiniz. Özel eşleme sırasında adreslerin diğer müşterilerle çakışmasını önlemek için trafiğinizin uçtan uca yalıtılmasını sağlarız. Bu adresler tanıtılan tooInternet değildir. 

### <a name="public-peering"></a>Ortak Eşleme

Hello Azure ortak eşleme yolu ortak IP adresleri Azure'da barındırılan, tooconnect tooall hizmetleri sağlar. Hello listelenen hizmetleri bunlar [ExpessRoute hakkında SSS](expressroute-faqs.md) ve Microsoft Azure üzerinde ISV'ler tarafından barındırılan tüm hizmetleri. Bağlantı tooMicrosoft Azure hizmetleri genel eşliği her zaman başlatıldığında ağınızdan hello Microsoft ağına doğru. Merhaba trafik hedefleyen tooMicrosoft ağ için genel IP adresleri kullanmanız gerekir.

### <a name="microsoft-peering"></a>Microsoft Eşlemesi

Merhaba Microsoft eşleme yolu hello Azure ortak eşleme yolu desteklenmeyen tooMicrosoft bulut Hizmetleri bağlanmanıza olanak sağlar. Exchange Online, SharePoint Online, Skype Kurumsal ve Dynamics 365 gibi Office 365 Hizmetleri Hello hizmetleri içerir. Microsoft, hello Microsoft eşlemesi üzerinde çift yönlü bağlantıyı destekler. Giden trafiğe tooMicrosoft bulut Hizmetleri, hello Microsoft ağına girmeden önce geçerli bir ortak IPv4 adresi kullanmanız gerekir.

IP adresi ve AS numarasının emin olun aşağıda listelenen hello kayıt defterleri birinde kayıtlı tooyou şunlardır.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> Genel IP adresleri tanıtılan tooMicrosoft ExpressRoute üzerinden tanıtılan toohello Internet olmamalıdır. Bu bağlantı tooother Microsoft Hizmetleri kesilebilir. Ancak ağınızda Microsoft içindeki O365 uç noktalarıyla iletişim kuran sunucular tarafından kullanılan Genel IP adresleri, ExpressRoute üzerinden tanıtılabilir. 
> 
> 

## <a name="dynamic-route-exchange"></a>Dinamik yönlendirme değişimi

Yönlendirme değişimi bir eBGP protokolü üzerinden olacaktır. EBGP oturumları hello Msee'ler ile yönlendiricileriniz arasında oluşturulur. BGP oturumlarının kimlik doğrulaması zorunlu değildir. Gerekirse bir MD5 karması yapılandırılabilir. Merhaba bkz [yönlendirmeyi yapılandırma](expressroute-howto-routing-classic.md) ve [hattı sağlama iş akışları ve devre durumları](expressroute-workflows.md) BGP oturumlarını yapılandırma hakkında bilgi.

## <a name="autonomous-system-numbers"></a>Otonom Sistem numaraları

Microsoft Azure genel, Azure özel ve Microsoft eşlemesi için AS 12076 kullanır. Asn'ler biz gelen 65515 too65520 iç kullanım için ayrılmıştır. Hem 16 hem de 32 bit AS numaraları desteklenir.

Veri aktarımı simetrisi etrafında bir gereksinim yoktur. Merhaba İleri ve geri dönüş yolları farklı yönlendirici çiftlerinden geçiş yapabilir. Aynı yollar size ait birden fazla devre çiftinin her iki tarafından tanıtılmalıdır. Yol ölçümlerinin gerekli toobe aynı değildir.

## <a name="route-aggregation-and-prefix-limits"></a>Yol toplama ve ön ek sınırları

Too4000 destekliyoruz toous hello Azure özel eşleme aracılığıyla tanıtılan ön ekler. Bu too10, hello ExpressRoute premium eklentisi etkinse 000 önekleri artırılabilir. Biz too200 önekleri Azure genel için BGP oturumu başına ve Microsoft eşlemesi kabul eder. 

Hello öneklerini sayısı hello sınırını aşarsa hello BGP oturumu düşürülür. Biz hello özel eşleme bağlantısı yalnızca varsayılan yolların kabul eder. Sağlayıcısı varsayılan rota ve hello Azure genel özel IP adreslerini (RFC 1918) ve Microsoft eşleme yollarındaki filtre gerekir. 

## <a name="transit-routing-and-cross-region-routing"></a>Geçiş yönlendirme ve çapraz bölge yönlendirme

ExpressRoute geçiş yönlendirici olarak yapılandırılamaz. Geçiş yönlendirme hizmetleri için bağlantı sağlayıcınızı toorely sahip olur.

## <a name="advertising-default-routes"></a>Varsayılan yolları tanıtma

Varsayılan yollar yalnızca Azure özel eşleme oturumlarında kullanılabilir. Böyle bir durumda, biz hello ilişkili sanal ağlar tooyour ağdan gelen tüm trafiğin yönlendirir. Varsayılan yolların özel eşlemede tanıtılması engellenme Azure hello Internet yolunun neden olur. Kurumsal edge tooroute trafiğinden Bel gerekir ve toohello Internet Hizmetleri için Azure üzerinde barındırılan. 

 tooenable bağlantı tooother Azure Hizmetleri ve altyapı hizmetleri, aşağıdaki öğelerindeki hello biri yerinde emin olmalısınız:

* Etkin tooroute trafiği toopublic uç noktaları olan Azure ortak eşleme
* Her alt ağ gerektiren Internet bağlantısı için kullanıcı tanımlı yönlendirme tooallow internet bağlantısı kullanın.

> [!NOTE]
> Varsayılan yolların tanıtılması, Windows ve diğer VM lisans etkinleştirmelerini bozar. Yönergeleri izleyerek [burada](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) bu geçici toowork.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>BGP toplulukları desteği (Önizleme)

Bu bölüm BGP toplulukların ExpressRoute ile nasıl kullanıldığına genel bir bakış sağlar. Microsoft yollar hello ortak ve Microsoft eşleme yollarındaki rotaları uygun topluluk değerleriyle etiketleyerek tanıtır. Bunu yapmak için stratejinin hello ve topluluk değerlerini aşağıda açıklanan ilgili ayrıntılar hello. Microsoft, ancak dikkate almayabilir hiçbir topluluk değerlerini etiketli tooroutes tanıtılan tooMicrosoft.

Coğrafi bölge içindeki herhangi bir eşleme konumundan ExpressRoute aracılığıyla tooMicrosoft bağlanıyorsanız hello jeopolitik sınır dahilindeki tüm bölgelerde erişim tooall Microsoft bulut Hizmetleri gerekir. 

Örneğin, tooMicrosoft amsterdam'da ExpressRoute aracılığıyla bağlandıysanız Kuzey Avrupa ve Batı Avrupa'da barındırılan erişim tooall Microsoft bulut hizmetlerine olacaktır. 

Toohello başvuran [ExpressRoute ortakları ve eşleme konumları](expressroute-locations.md) jeopolitik bölgeler, ilişkili Azure bölgeleri ve karşılık gelen ExpressRoute eşleme konumlarını ayrıntılı bir listesi için sayfa.

Bir jeopolitik bölge için birden fazla ExpressRoute devresi satın alabilirsiniz. Birden fazla bağlantıya sahip sunar, yüksek kullanılabilirliğe ilişkin önemli avantajlar son toogeo artıklık. Birden fazla ExpressRoute devrenizin olduğu durumlarda Microsoft hello ortak eşleme ve Microsoft eşleme yollarında hello öneklerini aynı kümesini tanıtılan alırsınız. Bu durum ağınız ile Microsoft arasında birden fazla yol olacağı anlamına gelir. Bu, büyük olasılıkla ağınızın içinde en iyi olmayan yönlendirme kararlarına toobe neden olabilir. Sonuç olarak, iyinin altında bağlantı deneyimleri toodifferent Hizmetleri karşılaşabilirsiniz. 

Microsoft ortak eşleme aracılığıyla tanıtılan ön eklere ve hello bölge hello öneklerini belirten uygun BGP topluluk değerlerini Microsoft içinde barındırılır. Merhaba topluluk değerlerini toomake uygun yönlendirme kararlarını toooffer üzerinde güvenebilirsiniz [en iyi yönlendirme toocustomers](expressroute-optimize-routing.md).

| **Jeopolitik Bölge** | **Microsoft Azure bölgesi** | **BGP topluluk değeri** |
| --- | --- | --- |
| **Kuzey Amerika** | | |
| Doğu ABD |12076:51004 | |
| Doğu ABD 2 |12076:51005 | |
| Batı ABD |12076:51006 | |
| Batı ABD 2 |12076:51026 | |
| Batı Orta ABD |12076:51027 | |
| Orta Kuzey ABD |12076:51007 | |
| Orta Güney ABD |12076:51008 | |
| Orta ABD |12076:51009 | |
| Orta Kanada |12076:51020 | |
| Doğu Kanada |12076:51021 | |
| **Güney Amerika** | | |
| Güney Brezilya |12076:51014 | |
| **Avrupa** | | |
| Kuzey Avrupa |12076:51003 | |
| Batı Avrupa |12076:51002 | |
| **Asya Pasifik** | | |
| Doğu Asya |12076:51010 | |
| Güneydoğu Asya |12076:51011 | |
| **Japonya** | | |
| Japonya Doğu |12076:51012 | |
| Japonya Batı |12076:51013 | |
| **Avustralya** | | |
| Avustralya Doğu |12076:51015 | |
| Avustralya Güneydoğu |12076:51016 | |
| **Hindistan** | | |
| Hindistan Güney |12076:51019 | |
| Hindistan Batı |12076:51018 | |
| Hindistan Orta |12076:51017 | |

Microsoft tarafından tanıtılan tüm yollar hello uygun topluluk değeriyle etiketlenecektir. 

> [!IMPORTANT]
> Genel ön ekler uygun bir topluluk değeri ile etiketlenecek ve yalnızca ExpressRoute premium eklentisi etkinleştirildiğinde tanıtılacaktır.
> 
> 

Ayrıca toohello yukarıdaki, Microsoft de ait hello hizmet göre ön eklere. Bu, yalnızca toohello Microsoft eşlemesi geçerlidir. Merhaba tabloda hizmet tooBGP topluluk değeri eşlenmesini sağlar.

| **Hizmet** | **BGP topluluk değeri** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **Skype Kurumsal** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **Diğer Office 365 Hizmetleri** |12076:5100 |

> [!NOTE]
> Microsoft hello yollar tanıtılan tooMicrosoft ayarladığınız hiçbir BGP topluluk değerini dikkate almaz.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar

* ExpressRoute bağlantınızı yapılandırın.
  
  * [Merhaba Klasik dağıtım modeli için ExpressRoute devresi oluşturma](expressroute-howto-circuit-classic.md) veya [oluşturma ve Azure Resource Manager kullanarak ExpressRoute devresi değiştirme](expressroute-howto-circuit-arm.md)
  * [Yapılandırma hello Klasik dağıtım modeli için yönlendirmeyi](expressroute-howto-routing-classic.md) veya [hello Resource Manager dağıtım modeli için yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md)
  * [Klasik bir VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md) veya [Resource Manager Vnet'i tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md)

